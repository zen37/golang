If you’re not using the Gorilla Mux router, there are several other options available for routing in Go. Here are some common alternatives:

### 1. **Standard Library `http.ServeMux`**

The Go standard library provides a simple router called `http.ServeMux`. It’s built into the `net/http` package and is suitable for basic routing needs.

**Example:**

```go
func New() http.Handler {
    mux := http.NewServeMux()
    mux.HandleFunc("/package/", packageHandler) // Handle all paths starting with /package/
    return mux
}
```

### 2. **Chi**

Chi is a lightweight, idiomatic router for Go, which is known for its simplicity and performance.

**Installation:**

```sh
go get github.com/go-chi/chi/v5
```

**Example:**

```go
import "github.com/go-chi/chi/v5"

func New() http.Handler {
    r := chi.NewRouter()
    r.Get("/package/{package}/{version}", packageHandler)
    return r
}
```

### 3. **Echo**

Echo is a high-performance, extensible web framework for Go.

**Installation:**

```sh
go get github.com/labstack/echo/v4
```

**Example:**

```go
import "github.com/labstack/echo/v4"

func New() http.Handler {
    e := echo.New()
    e.GET("/package/:package/:version", packageHandler)
    return e
}
```

### 4. **Gin**

Gin is a fast and feature-rich web framework for Go, known for its performance and flexibility.

**Installation:**

```sh
go get github.com/gin-gonic/gin
```

**Example:**

```go
import "github.com/gin-gonic/gin"

func New() http.Handler {
    r := gin.Default()
    r.GET("/package/:package/:version", packageHandler)
    return r
}
```

### 5. **Fiber**

Fiber is an expressive and fast web framework inspired by Express.js for Go.

**Installation:**

```sh
go get github.com/gofiber/fiber/v2
```

**Example:**

```go
import "github.com/gofiber/fiber/v2"

func New() http.Handler {
    app := fiber.New()
    app.Get("/package/:package/:version", packageHandler)
    return app
}
```

### Summary

- **`http.ServeMux`**: Simple and part of the Go standard library, suitable for basic routing.
- **Chi, Echo, Gin, Fiber**: Third-party libraries that offer more features and flexibility, suitable for more complex routing needs and additional features.

Choosing a router depends on your project’s requirements and complexity. For basic applications, `http.ServeMux` is often sufficient. For more advanced needs, libraries like Chi, Echo, Gin, or Fiber provide additional capabilities and improved performance.

Using `github.com/gorilla/mux` offers several advantages over the standard `http.NewServeMux`, particularly if your application requires more advanced routing features. Here are some key reasons why you might prefer `gorilla/mux`:

### Advantages of `gorilla/mux`

1. **Path Variables**:
   - `mux` supports defining and extracting path variables directly in the route definition, making it easy to capture and use parts of the URL in your handlers. For example, you can define routes like `/{package}` or `/users/{id:[0-9]+}` and easily access these variables in your handlers.

2. **Request Method Matching**:
   - You can specify which HTTP methods (GET, POST, etc.) a route should handle. This is useful for RESTful APIs where different methods on the same URL might trigger different behaviors.

3. **Route Prioritization**:
   - `mux` allows you to define routes in a specific order, ensuring that more specific routes are matched before more general ones.

4. **Middleware Support**:
   - `mux` provides easy integration with middleware, allowing you to run specific functions before or after your handlers.

5. **Subrouters**:
   - You can create subrouters with `mux`, which can be useful for grouping routes that share common middleware or path prefixes.

6. **Path Prefixes and Suffixes**:
   - `mux` supports matching routes with prefixes (`PathPrefix`) and suffixes, offering more flexible routing options.

7. **Host-based Routing**:
   - You can route requests based on the host header, which is useful for applications that need to handle multiple domains.

### When to Use `http.NewServeMux`

- **Simple Applications**: If your routing needs are simple and you don't require the advanced features offered by `mux`, `http.NewServeMux` can be a lightweight and sufficient choice.
- **Built-in and Minimal**: `http.NewServeMux` is part of the standard library, so it doesn't require any third-party dependencies. This can be a plus for projects that aim to minimize dependencies.

### Conclusion

For most applications, especially those with complex routing requirements, `gorilla/mux` provides a more powerful and flexible routing solution compared to the standard `http.NewServeMux`. However, for simple use cases where advanced routing features are not needed, `http.NewServeMux` might be a better fit due to its simplicity and zero-dependency nature. Ultimately, the choice depends on the specific needs and complexity of your application.