# Basic routing

For each route you will need to provide a `method`, a `path`, an `handler` (and eventually a `name`).

> [!INFO]
>
> The `handler` can only be a **string** that will be in used in the container to retrieve an
> instance of the handler.  
> 
> Usually the FQCN of the handler is used (for example `HomeHandler::class`) so that the auto-wiring
> of the container can find it easily.

The Borsch application provides those methods to define a route :

- `get()`
- `post()`
- `put()`
- `patch()`
- `delete()`
- `match()`
- `any()`

## Create a GET route

You can add a route that handles only GET HTTP requests with the Borsch router's `get()` method.  
It accepts three arguments:

- The route path
- The route handler
- The route name (optional)

```php
$app->get('/', HomeHandler::class, 'home');
```

## Create a [POST|PUT|PATCH|DELETE] route

As the `get()` method, you can add a route that handles only POST or PUT or PATCH or DELETE HTTP
requests with the Borsch router's `post()`, `put()`, `patch()`, `delete()` methods.  
It accepts three arguments:

- The route path
- The route handler
- The route name (optional)

```php
$app->post('/', HomeHandler::class, 'home');
$app->put('/', HomeHandler::class, 'home');
$app->patch('/', HomeHandler::class, 'home');
$app->delete('/', HomeHandler::class, 'home');
```

## Create a multiple method route

If you need a route to handle multiple HTTP methods, you can use the `match()` method.  
It accepts four arguments:

- An array of HTTP methods (can be an array of **string** or `HttpMethods` enum)
- The route path
- The route handler
- The route name (optional)

```php
$app->match(['POST', 'PUT'], '/orders', OrderHandler::class, 'orders');

// With HttpMethods enum
$app->match([HttpMethods::POST, HttpMethods::PUT], '/orders', OrderHandler::class, 'orders');
```

## Create a route for any HTTP method

If you want a route that accept any HTTP method, you can use the `any()` method.  
It accepts three arguments:

- The route path
- The route handler
- The route name (optional)

```php
$app->any('/', HomeHandler::class, 'home');
```