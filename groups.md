# Groups

To avoid repeating the same url segment for multiple routes, groups allow you to share it without
needing to define the url segment on each individual route.

You can use the `group()` method.  
It accepts two arguments:

- The group path segment
- A callback function containing the routes of the group

```php
$app->group('/grouped/path', function (App $app) {
    $app->group('/to', function (App $app) {
        $app->get('/get', TestHandler::class); // https://example.com/grouped/path/to/get
    });
});
```
