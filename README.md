# cakephp-4-tutorial

## Overview
Build cakephp development with docker for CakePHP official tutorials.  
https://book.cakephp.org/4/en/tutorials-and-examples.html

* nginx:1.18-alpine
* php:7.4-fpm-buster
* mysql:8

Check the official CakePHP manual.
* [installation](https://book.cakephp.org/4/en/installation.html)
* [quickstart](https://book.cakephp.org/4/en/quickstart.html)

## Build

Build docker containers and start a CakePHP project.
```bash
$ mkdir -p my_project && cd $_
$ git clone git@github.com:zakbutchy/cakephp-4-tutorial.git
$ cd docker/
$ docker-compose up -d

# If you want to install the another version, run the following command in cake4-php container
$ docker exec -it cake4-php bash
/var/www/html# rm -rf app/
/var/www/html# composer self-update
/var/www/html# composer create-project --prefer-dist cakephp/app:<version number> app
... composer install ...
/var/www/html# exit
```

## Fix configurations

Duplicate env.example and edit env as below.
```sh
cp ./config/.env.example ./config/.env
```

config/.env
```sh
export DB_HOST="cake4-mysql"
export DB_SCHEMA="cake_cms"
export DB_USERNAME="cakephp"
export DB_PASSWORD="password"
```

Uncomment this block in config/bootstrap.php to enable the env file.
```php
if (!env('APP_NAME') && file_exists(CONFIG . '.env')) {
    $dotenv = new \josegonzalez\Dotenv\Loader([CONFIG . '.env']);
    $dotenv->parse()
        ->putenv()
        ->toEnv()
        ->toServer();
}
```

Replace the values below config/app_local.php
```php
'Datasources' => [
    'default' => [
        'host' => env('DB_HOST', 'localhost'),
        'username' => env('DB_USERNAME', ''),
        'password' => env('DB_PASSWORD', ''),
        'database' => env('DB_SCHEMA', ''),
        // more configurations...
    ],
],
```

Also refer to this document.  
https://book.cakephp.org/4/en/tutorials-and-examples/cms/database.html#id1

## Access
Welcome to CakePHP  
http://0.0.0.0:8080
