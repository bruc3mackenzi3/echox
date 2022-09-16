+++
title = "Basic Auth Middleware"
description = "Basic auth middleware for Echo"
[menu.main]
  name = "Basic Auth"
  parent = "middleware"
+++

Basic auth middleware provides an HTTP basic authentication.

- For valid credentials it calls the next handler.
- For missing or invalid credentials, it sends "401 - Unauthorized" response.

*Usage*

```go
e.Use(middleware.BasicAuth(func(username, password string, c echo.Context) (bool, error) {
	// Be careful to use constant time comparison to prevent timing attacks
	if subtle.ConstantTimeCompare([]byte(username), []byte("joe")) == 1 &&
		subtle.ConstantTimeCompare([]byte(password), []byte("secret")) == 1 {
		return true, nil
	}
	return false, nil
}))
```

## Custom Configuration

*Usage*

```go
e.Use(middleware.BasicAuthWithConfig(middleware.BasicAuthConfig{}))
```

## Configuration

Configuration is done via the `BasicAuthConfig` struct type. For full details see the [BasicAuthConfig Go Doc](https://pkg.go.dev/github.com/labstack/echo/v4/middleware#BasicAuthConfig).

*Default Configuration*

```go
DefaultBasicAuthConfig = BasicAuthConfig{
	Skipper: DefaultSkipper,
}
```
