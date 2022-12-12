# REST Handler

REST handler is a package to handle API REST requests. this package is responsible to route REST API request, set middleware in group or each API route, parse API request `URL query param` and/or `request body` into variables or struct, may or may not as first layer of API request validation (depends on API responsibily if necessary), and pass the parsed struct or variables to usecase.

- ### Api Routes :
  
  to route api path go to `{your_module}/delivery/rest/resthandler.go` file and set api path routes within `Mount` function. all of  the routes will be registered and can be accessed. example of REST handler routing implementation :
  ```go
    func (h *RestHandler) Mount(root *echo.Group) {
        order := root.Group("order")
        order.GET("", h.getAllOrder)
        order.POST("", h.createOrder)
        order.PUT("/:orderId", h.updateOrder)
    }
  ```
  it will be mounted and registered as 3 API routes when application run :

  `**GET** {your_host}/order`

  `**POST** {your_host}/order`

  `**PUT** {your_host}/order/{orderId}`

- ### Handling Request :
  
  each REST API route must have a handler function. for example :
  - Handling URL Query Request (GET) :
  ```go
    // FilterOrder : this is just an example of parsing request to struct,
    // this struct should be created in domain package inside a module
    type FilterOrder struct {
        Search string `json:"string"`
        ID     string `json:"id"`
        Page   int `json:"page"`
        Limit  int `json:"limit"`
    }
    func (h *RestHandler) getAllOrder(c echo.Context) error {
        trace, ctx := tracer.StartTraceWithContext(c.Request().Context(), "OrderDeliveryREST:GetAllOrder")
        defer trace.Finish()

        var filter FilterOrder
        if err := candihelper.ParseFromQueryParam(c.Request().URL.Query(), &filter); err != nil {
            return wrapper.NewHTTPResponse(http.StatusBadRequest, "Failed parse filter", err).JSON(c.Response())
        }

        data, meta, err := h.uc.Order().GetAllOrder(ctx, &filter) // proceed request
        if err != nil {
            return wrapper.NewHTTPResponse(http.StatusBadRequest, err.Error()).JSON(c.Response())
        }

        return wrapper.NewHTTPResponse(http.StatusOK, "success", meta, data).JSON(c.Response())
    }
  ```

  - Handling Body Request (PUT/POST/PATCH) :
  ```go
    // RequestOrder : this is just an example of parsing request to struct,
    // this struct should be created in domain package inside a module
    type RequestOrder struct {
        ID    string `json:"id"`
        ReferenceNumber  string `json:"referenceNumber"`
        Price  float64 `json:"price"`
    }
    func (h *RestHandler) updateOrder(c echo.Context) error {
        trace, ctx := tracer.StartTraceWithContext(c.Request().Context(), "OrderDeliveryREST:UpdateOrder")
        defer trace.Finish()

        body, _ := io.ReadAll(c.Request().Body)
        var payload RequestOrder
        if err := json.Unmarshal(body, &payload); err != nil {
            return wrapper.NewHTTPResponse(http.StatusBadRequest, err.Error()).JSON(c.Response())
        }

        payload.ID = c.Param("orderId") // this should match within routes param, in this case is :orderId
        err := h.uc.Order().UpdateOrder(ctx, &payload) // proceed request
        if err != nil {
            return wrapper.NewHTTPResponse(http.StatusBadRequest, err.Error()).JSON(c.Response())
        }

        return wrapper.NewHTTPResponse(http.StatusOK, "Success").JSON(c.Response())
    }
  ```

- ### Validation
  <a href="#/service/api/jsonschema/">See JSONSchema validation </a>