# Configuration

The Borsch Framework skeleton is quite easy to understand and modify according to your needs (even
though it should not be necessary).

## Public directory

After installing Borsch Skeleton, configure your web server's root to be the `public` directory.  
The `index.php` and `worker.php` (FrankenPHP worker mode) are the entry points for all HTTP
requests of your application.

## Environment file

When installed via Composer `create-project` command line, a `.env` file is automatically generated
in the root folder of your application.  

If you did not use `create-project` command line then copy the `.env.example` file and rename it as
`.env`.  
Typically: `cp .env.example .env`.

Review the default environment variable, update them, add your own, add a proper `APP_KEY` if
not done yet during the `create-project` command.

## Permissions

Make sure directories within `storage` directory are writable by your web server, or it will not run.
