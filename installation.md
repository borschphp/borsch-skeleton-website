# Installation

## Requirements

- PHP 8.2+
- [Composer](https://getcomposer.org)

## Create a new project

Use the Composer's create-project command:

```bash
composer create-project borschphp/skeleton <app-name>
```

## Run it

```bash
composer serve
```

Then go to [0.0.0.0:8080](http://0.0.0.0:8080) to see the welcome page of your project.

It is also possible to run it via [FrankenPHP](https://frankenphp.dev), in worker mode.  
You'll need to have [Docker](https://www.docker.com/) installed and up to use this command :

```bash
composer franken
```

Then go to [https://localhost](https://localhost) (where you'll need to accept self-signed certificate).
