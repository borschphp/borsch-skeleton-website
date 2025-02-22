# Pipeline

The pipeline is the heart of your application and consist of a sequence of Middlewares.  
Every request goes through the pipeline until a [PSR-7 ResponseInterface](https://www.php-fig.org/psr/psr-7/)
is returned.

The default pipeline should be good as is and should not require many changes to comply to your need.

The `./config/pipeline.php` file is well documented, have a look at it if you need more information.

## Piping a Middleware

To add a Middleware to the pipeline, you can use the `pipe()` method of the `App` object.
When you pipe middleware to the application, it is added to a queue, and dequeued in order until a middleware returns
a response instance.

Here is an example of how to pipe a middleware:

```php
$app->pipe(ErrorHandlerMiddleware::class);
```

In this example, the `ErrorHandlerMiddleware` will be called for every request.

## Piping a Middleware with a path segregation

You can also pipe a middleware to a specific path. This is useful when you want to apply a middleware only to a specific
route.

Here is an example of how to pipe a middleware to a specific path:

```php
$app->pipe('/api', BodyParserMiddleware::class);
```

In this example, the `BodyParserMiddleware` will only be called for requests to the `/api` path.

You can also provide an array of middleware classes:

```php
$app->pipe('/api', [
    BodyParserMiddleware::class,
    UploadedFilesParserMiddleware::class
]);
```

In this example, the `BodyParserMiddleware` and `UploadedFilesParserMiddleware` will only be called for requests to the
`/api` path.