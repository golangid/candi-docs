# Usecase

### Usecase is a package to handle specific business logic of specific module. 

Usecase has responsibilities to validate request (optional), validate data from database, create requested response to client (handler). usecase may or may not have more third party dependencies in it.

### Usecase dependencies :
1. shared usecase to call other module's usecases.
2. shared repo or repository to access data from database.
3. kafka publisher to publish kafka messages.
4. cache to get or store data to redis.

> External dependencies should be set in config using dependency.SetExtended(map[string]interface{})

Set singleton dependencies in `configs/configs.go`
```go
deps = dependency.InitDependency(
	dependency.SetExtended(map[string]interface{}{"external_deps_key" : plugins.New()}),
)
```

> This will keep your code clean and easier to mock dependencies by doing singleton dependency injection instead of creating new object for each function call inside usecase.

To access it set in `usecase.go` file of specific module that will use the dependencies.
```go
type orderUsecaseImpl struct {
	sharedUsecase common.Usecase
	repoSQL       repository.RepoSQL
    plugins       plugins.Plugin
}

func NewOrderUsecase(deps dependency.Dependency) (OrderUsecase, func(sharedUsecase common.Usecase)) {
	uc := &orderUsecaseImpl{
		repoSQL: repository.GetSharedRepoSQL(),
        // get the deps with key and cast the interface value to specific deps
        plugins:  deps.GetExtended("external_deps_key").(plugins.Plugin),
	}
	return uc, func(sharedUsecase common.Usecase) {
		uc.sharedUsecase = sharedUsecase
	}
}
```

### Example of usecase implementation :

1. User wants to update specific data order.
2. Validate given data id or code exists in database.
3. Update data and its relation then commit. 
4. publish data to kafka.

```go
package usecase

import (
	"fmt"
	"context"
    "errors"

	"gorm.io/gorm"

	"github.com/golangid/candi/tracer"
	"github.com/golangid/candi/candishared"
)

func (uc *orderUsecaseImpl) UpdateOrder(ctx context.Context, request RequestOrder) (err error) {
	// create span context in jaeger tracing
	trace, ctx := tracer.StartTraceWithContext(ctx, "OrderUsecase:UpdateOrder")
	defer trace.Finish()

    // check existing order
	repoFilter := FilterOrder{
        OrderNumber: request.OrderNumber, 
        Preloads: []string{"Items"}, // see repository doc.
    }
	order, err := uc.repoSQL.OrderRepo().Find(ctx, repoFilter)
	if err != nil {
		if errors.Is(err, gorm.ErrRecordNotFound) {
			err = fmt.Errorf("invalid order number. order number '%s' not found", request.OrderNumber)
		}
		return err
	}

    // replace old order items.
	order.Items = make([]OrderItem, 0)
	for _, item := range request.Items {
		Order.Items = append(Order.Items, OrderItem{
			OrderNumber: request.OrderNumber,
			Name: item.Name,
			Price: item.Price,
		})
	}

	// candi built in with transaction function
	// if err returned it will rollback the database transaction
	err = uc.repoSQL.WithTransaction(ctx, func(ctx context.Context) error {
		// delete all exisiting order items
		if err = uc.repoSQL.OrderItemRepo().Delete(ctx, FilterOrderItem{OrderNumber: request.OrderNumber}); err != nil {
			return err
		}
		// save order items relation
		if err = uc.repoSQL.OrderItemRepo().SaveBulk(ctx, &order.Items); err != nil {
			return err
		}
		// save order
		return uc.repoSQL.OrderItem().Save(ctx, &order)
	})
    // check if transaction has error (rolled back) and return before publishing messages when error occurs.
	if err != nil {
		return err
	}

    // publish updated order
	if err = uc.kafkaPub.PublishMessage(ctx, &candishared.PublisherArgument{
		Topic:   "Kafka-Topic",
		Key:     order.RequestNumber,
		Data:    order,
	}); err != nil {
		// recomended to log or send notification the error and kafka arguments, 
        // so it can be published manually when error occurs.
		return nil
	}

	return nil
}
```

Given example filter and models :
```go


// FilterOrder payload
type FilterOrder struct {
	candishared.Filter
	ID           uint64 `json:"id"`
    OrderNumber  string `json:"orderNumber"`
    Preloads   []string `json:"-"`
}

// FilterOrderItem payload
type FilterOrderItem struct {
	ID           uint64  `json:"id"`
	Name         string  `json:"name"`
    OrderNumber  string  `json:"orderNumber"`
}

// RequestOrder payload
type RequestOrder struct {
	ID           uint64             `json:"id"`
    OrderNumber  string             `json:"orderNumber"`
	Items        []RequestOrderItem `json:"field"`
}

// RequestOrderItem payload
type RequestOrderItem struct {
	ID           uint64  `json:"id"`
	Name         string  `json:"name"`
    Price        float64 `json:"price"`
    OrderNumber  string  `json:"orderNumber"`
}

// Order database model
type Order struct {
    ID           uint64      `gorm:"id"`
    OrderNumber  string      `gorm:"orderNumber"`
    Items        []OrderItem `gorm:"foreignKey:OrderNumber"`
}

// OrderItem database model
type OrderItem struct {
	ID           uint64  `gorm:"id"`
	Name         string  `gorm:"name"`
    OrderNumber  string  `gorm:"orderNumber"`
    Price        float64 `gorm:"price"`
}
```