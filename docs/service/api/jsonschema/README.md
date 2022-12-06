# JSON Schema

JSON schema *(optional)* is json file with request payload definition. JSON Schema meant to use as API request validation and the first layer of handling incoming request before processing the request values.

JSON schema implementation :

- **JSON Schema files**
  
  it is recomended to create new folder with your specific API module's name.

  example api request validation to get all orders :

  *default jsonschema error message can be overrided with **message** key inside specific property*
  <img src="assets/jsonschema-structure.png" />

```json
    {
        "$schema": "http://json-schema.org/draft-07/schema",
        "title": "get all orders",
        "type": "object",
        "additionalProperties": true,
        "properties": {
            "page": {
                "type": "number",
                "minimum": 1,
                "message" : "page should be numeric with minimum 1"
            },
            "limit": {
                "type": "number",
                "minimum": 1,
                "message" : "limit should be numeric with minimum 1"
            },
            "orderBy": {
                "type": "string",
                "enum": ["id", "field", "createdAt", "updatedAt"]
            },
            "sort": {
                "type": "string",
                "enum": ["asc", "desc", "ASC", "DESC"]
            },
            "search": {
                "type": "string"
            },
            "startDate": {
                "anyOf": [
                    {
                        "type": "string",
                        "format": "date"
                    },
                    {
                        "type": "string",
                        "maxLength": 0
                    }
                ]
            },
            "endDate": {
                "anyOf": [
                    {
                        "type": "string",
                        "format": "date"
                    },
                    {
                        "type": "string",
                        "maxLength": 0
                    }
                ]
            }
        }
    }
```

- **JSON Schema validation**
  - **GET** request (Query Parameter) :
    1. parse URL query parameter in handler / delivery
    ```go
        var filter domain.FilterOrder
        if err := candihelper.ParseFromQueryParam(c.Request().URL.Query(), &filter); err != nil {
            return wrapper.NewHTTPResponse(http.StatusBadRequest, "Failed parse filter", err).JSON(c.Response())
        }
    ```
    2. validate :
    ```go
        if err := h.validator.ValidateDocument("order/get_all", filter); err != nil {
		return wrapper.NewHTTPResponse(http.StatusBadRequest, "Failed validate filter", err).JSON(c.Response())
	    }
    ```   

    complete example handler code :
    ```go
    func (h *RestHandler) getAllOrder(c echo.Context) error {
        trace, ctx := tracer.StartTraceWithContext(c.Request().Context(), "OrderDeliveryREST:GetAllOrder")
        defer trace.Finish()

        var filter domain.FilterOrder
        if err := candihelper.ParseFromQueryParam(c.Request().URL.Query(), &filter); err != nil {
            return wrapper.NewHTTPResponse(http.StatusBadRequest, "Failed parse filter", err).JSON(c.Response())
        }

        if err := h.validator.ValidateDocument("order/get_all", filter); err != nil {
            return wrapper.NewHTTPResponse(http.StatusBadRequest, "Failed validate filter", err).JSON(c.Response())
        }

        data, meta, err := h.uc.Order().GetAllOrder(ctx, &filter)

        if err != nil {
            return wrapper.NewHTTPResponse(http.StatusBadRequest, err.Error()).JSON(c.Response())
        }

        return wrapper.NewHTTPResponse(http.StatusOK, "success get all orders", meta, data).JSON(c.Response())
    }
    ```

  - **POST/PUT** request (Query Parameter) :
      1. validate
      ```go
          body, _ := io.ReadAll(c.Request().Body)
          if err := h.validator.ValidateDocument("order/save", body); err != nil {
            return wrapper.NewHTTPResponse(http.StatusBadRequest, "Failed validate payload", err).JSON(c.Response())
          }
      ``` 

      2. parse body request in handler / delivery :
      ```go
          var payload domain.RequestOrder
          if err := json.Unmarshal(body, &payload); err != nil {
            return wrapper.NewHTTPResponse(http.StatusBadRequest, err.Error()).JSON(c.Response())
          }
      ```

      complete example handler code :
      ```go
        func (h *RestHandler) createOrder(c echo.Context) error {
            trace, ctx := tracer.StartTraceWithContext(c.Request().Context(), "OrderDeliveryREST:CreateOrder")
            defer trace.Finish()

            body, _ := io.ReadAll(c.Request().Body)
            if err := h.validator.ValidateDocument("order/save", body); err != nil {
                return wrapper.NewHTTPResponse(http.StatusBadRequest, "Failed validate payload", err).JSON(c.Response())
            }

            var payload domain.RequestOrder
            if err := json.Unmarshal(body, &payload); err != nil {
                return wrapper.NewHTTPResponse(http.StatusBadRequest, err.Error()).JSON(c.Response())
            }

            err := h.uc.Order().CreateOrder(ctx, &payload)
            if err != nil {
                return wrapper.NewHTTPResponse(http.StatusBadRequest, err.Error()).JSON(c.Response())
            }

            return wrapper.NewHTTPResponse(http.StatusOK, "Success").JSON(c.Response())
        }
      ```