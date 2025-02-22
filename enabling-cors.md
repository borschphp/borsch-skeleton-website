# Enabling CORS

> Cross-origin resource sharing (CORS) is a mechanism that allows restricted resources on a web page to be requested from another domain outside the domain from which the first resource was served.
> - [Wikipedia](https://en.wikipedia.org/wiki/Cross-origin_resource_sharing)

It is usually recommended to set CORS directly in your web server, but if for some reason you want to deal with CORS in
PHP, here is the solution: **create a new middleware at the beginning of your pipeline**.

## The middleware

Create a new `CorsMiddleware` class in `src/Middleware/CorsMiddleware.php`.  
Insert the code below in your new middleware :

```php
namespace App\Middleware;

use Psr\Http\Message\{ResponseInterface, ServerRequestInterface};
use Psr\Http\Server\{MiddlewareInterface, RequestHandlerInterface};

class CorsMiddleware implements MiddlewareInterface
{

    /**
     * @inheritDoc
     */
    public function process(ServerRequestInterface $request, RequestHandlerInterface $handler): ResponseInterface
    {
        return $handler->handle($request)
            ->withHeader('Access-Control-Allow-Origin', '*')
            ->withHeader('Access-Control-Allow-Headers', 'X-Requested-With, Content-Type, Accept, Origin, Authorization')
            ->withHeader('Access-Control-Allow-Methods', 'GET, POST, PUT, DELETE, PATCH, OPTIONS');
    }
}
```

## In the pipeline

You need to place at the beginning of the timeline, after the error middleware, the new `CorsMiddleware`:

```php
return function (App $app): void {
    $app->pipe(ErrorHandlerMiddleware::class);

    // Place it here
    $app->pipe(CorsMiddleware::class);

    $app->pipe(TrailingSlashMiddleware::class);
    $app->pipe(ContentLengthMiddleware::class);
    // ...
};
```