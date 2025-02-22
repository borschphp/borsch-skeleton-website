# Borsch Framework

## Keep it simple.

Sometimes, you don't need an overkill solution like [Laravel](https://laravel.com/) or [Symfony](https://symfony.com/).

Borsch is a simple and efficient [PSR-15](https://www.php-fig.org/psr/psr-15) micro framework made to kick start your
web app or API development by using the tools you prefer, and provides minimal structure and facilities to ease your
development.

```php
<?php

namespace App\Handler;

use Borsch\Template\TemplateRendererInterface;
use Laminas\Diactoros\Response\HtmlResponse;
use Psr\Http\{Message\ResponseInterface, Message\ServerRequestInterface, Server\RequestHandlerInterface};

readonly class HomeHandler implements RequestHandlerInterface
{

    public function __construct(
        protected TemplateRendererInterface $engine
    ) {}

    public function handle(ServerRequestInterface $request): ResponseInterface
    {
        $this->engine->assign([
            'name' => ($request->getQueryParams()['name'] ?? $request->getHeaderLine('X-Name')) ?: 'World'
        ]);

        return new HtmlResponse($this->engine->render('home.tpl'));
    }
}
```

## Quick setup

The recommended way to install the Borsch Framework is with [Composer](https://getcomposer.org/).
Get started quick using [borsch-skeleton](https://github.com/borschphp/borsch-skeleton) as a starting point by running
the command :

```bash
composer create-project borschphp/borsch-skeleton [your-app-name]
```

Replace `[your-app-name]` with the name of your application.

You can then run it with PHP's built-in webserver :

```bash
# With built-in PHP server:
php -S 0.0.0.0:8080 -t ./public/ ./public/index.php

# Or with the composer script:
composer serve

# Or in FrankenPHP worker mode:
composer franken
```
You can then visit http://0.0.0.0:8080.

