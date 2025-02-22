# Overview

You can define your application's route in the files :
- 
- `./config/routes.php` (usually used for frontend)
- `./config/api.php` (usually used for backend)

Note that this skeleton uses a [nikic/FastRoute](https://github.com/nikic/FastRoute) implementation
router, so you can use the `FastRoute` patterns to define your app routes.

## Handlers

You need to provide a [PSR-15 Request Handler](https://www.php-fig.org/psr/psr-15) to each routes.  
The Request Handler will be in charge of generating a response for the matched route.

Example :

```php
namespace App\Handler;

use Laminas\Diactoros\Response\JsonResponse;
use Psr\Http\Message\ResponseInterface;
use Psr\Http\Message\ServerRequestInterface;
use Psr\Http\Server\RequestHandlerInterface;

class OrderHandler implements RequestHandlerInterface
{
    
    protected function get(ServerRequestInterface $request): ResponseInterface
    {
        return new JsonResponse([
            // Orders...
        ]);
    }
    
    protected function post(ServerRequestInterface $request): ResponseInterface
    {
        // Created order
        return new JsonResponse([]);
    }
    
    protected function put(ServerRequestInterface $request, int $order_id): ResponseInterface
    {
        // Update order
        return new JsonResponse([]);
    }
    
    protected function delete(ServerRequestInterface $request, int $order_id): ResponseInterface
    {
        // Delete order
        return new JsonResponse([]);
    }

    public function handle(ServerRequestInterface $request): ResponseInterface
    {
        $order_id = (int)$request->getAttribute('id');
        $method = strtolower($request->getMethod());
        
        if (!method_exists($this, $method)) {
            throw new \BadMethodCallException(sprintf(
                'Method %s::%s is unknown...',
                __CLASS__,
                $method
            ));
        }
        
        return $this->{$method}($request, $order_id);
    }
}
```

> [!INFO]
>
> Borsch skeleton is bundled with [Laminas Diactoros PSR-7](https://github.com/laminas/laminas-diactoros)
> implementation as you can see in this example.

## Names

You can specify a route name explicitly:

```php
// Here "home"
$app->get('/', HomeHandler::class, 'home');
```

Or let the router do it for you:

```php
// Here "GET^/"
$app->get('/', HomeHandler::class, 'home');

// Here "GET:POST^/user[/{id:\d+}]"
$app->match(['GET', 'POST'], '/user[/{id:\d+}]', UserHandler::class);
```

Internally (in `Borsch\Router\Route`), route names are determined like so:

```php
$this->name = sprintf(
    '%s^%s',
    implode(':', $this->methods),
    $this->path
);
```

> [!WARNING]
> 
> 2 routes cannot have the same name, or an exception will be thrown!

## Caching

By default, in a production environment, a cache file is generated in
`./storage/smarty/routes.cache.php`.  
You can modify this in the `./config/containers/app.container.php` file, in the
`RouterInterface::class` definition.

```php
$this
    ->getContainer()
    ->add(RouterInterface::class, function () {
        $router = new FastRouteRouter();
        if (isProduction()) {
            $router->setCacheFile(cache_path('routes.cache.php'));
        }

        return $router;
    });
```
