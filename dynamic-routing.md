# Dynamic routing

Dynamic routing is a way to pass parameters to a route. This is useful when you want to pass data to a route.
For example, you might want to pass an ID to a route to fetch data from a database.

## Placeholders

Here is an example of a dynamic route:

```php
$app->any('/albums/{id}', AlbumHandler::class, 'albums');
```

In this example, the `{id}` part of the route is a placeholder for the ID of the album. When a request is made to
`/albums/1`, the `AlbumHandler` class will be called with the ID `1`.

The value of the placeholder is passed to the handler as an attribute of the request object. You can access it like this:

```php
// In your handler
public function handle(ServerRequestInterface $request): ResponseInterface
{
    $id = (int)$request->getAttribute('id');
}
```

## Regular expressions

You can also specify a _regular expression_ to match the placeholder. For example, if you want to match only numbers, you can do this:

```php
$app->any('/albums/{id:\d+}', AlbumHandler::class, 'albums');
```

In this example, the `{id:\d+}` part of the route will only match numbers. If a request is made to `/albums/abc`, the route will not match.

## Optional placeholders

You can make a part of the route optional by placing it between blocks `[]`. For example:

```php
$app->any('/albums[/{id:\d+}]', AlbumHandler::class, 'albums');
```

In this example, the `{id}` part of the route is optional. If a request is made to `/albums`, the route will still match.

## Multiple placeholders

Of course, you can have multiple placeholders in a route. For example:

```php
$app->any('/albums/{artist_id}/{year}', AlbumHandler::class');
```

In this example, the route will match requests like `/albums/1/2022` or `/albums/2/2023`.

You can even combine optional and required placeholders:

```php
$app->any('/albums[/{artist_id:\d+}][/{year}]', AlbumHandler::class);
```

In this example, the route will match requests like `/albums/1/2022`, `/albums/1`, or `/albums`.