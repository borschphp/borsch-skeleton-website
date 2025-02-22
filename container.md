# Container

A Dependency Injection Container is used to define **application dependencies** (router, request handler,
server request factory and even the Application instance itself), middlewares and related dependencies.

The application is loaded from the container so its dependencies are automatically resolved.  The pipeline and
routes are then defined.  
The [PSR-15 Request Handler](https://www.php-fig.org/psr/psr-15/) is then run to return a
[PSR-7 ResponseInterface](https://www.php-fig.org/psr/psr-7/) to the client.

In the file `./config/container.php` you can find the application dependencies.  
For clarity, the container is filled with definitions in separated files in the `./config/containers` directory.

> [!NOTE]
>
> The container uses auto-wiring, so most of the time you do not even need to define your dependency, the container will
> resolve it by itself.