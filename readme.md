## Laravel Docker Soluion

Lighter alternative to LaraDock.

**Included Applications:**

- PHP with Apache
- Laravel Installation
- Composer
- MySQL
- PhpMyAdmin

## How to run

Install Docker or Docker Toolbox from http://www.docker.com

- Clone from Repository

- Change the working directory to the downloaded folder and run docker-compose up

```
docker-compose up
```

or run add the -d option to run it in background.

```
docker-compose up -d
```

This will boot up the machines and will start the installation of Laravel and composer packages. Once the installation is complete you will see the Laravel home page in localhost:8080 (or the port you specified in ENV).

Note: If you use docker toolbox, you might need to use the IP address of the docker machine rather than `localhost`

## App Folder

Laravel will be installed in a subfolder `app`.

## Database

MySql stores data in local folder `.db_data`. If you delete the folder database contents will be lost. You may ignore the database contents from .gitignore by uncommenting the line in `.git-ignore` file.

```
#To ignore local db changes you may uncomment the following line
#.db_data
```

Default user name is `root` with password `secret`

PhpMyAdmin can be accessed on http://localhost:8081 or the port you assigned in .env file

To connect from Laravel, use mysql as the host name in Laravel's .env file.

Eg:

```
DB_CONNECTION=mysql
DB_HOST=mysql
DB_PORT=3306
DB_DATABASE=lara
DB_USERNAME=root
DB_PASSWORD=secret
```

## Configuration

Edit the .env file and modify as necessary

```
#Select the PHP version

PHP_VERSION=7.2

#Select the MySql Tag. Defaults to latest
#Eg: 5.7

MYSQL_TAG=latest

#Databse and access details

DB_USERNAME=root
DB_PASSWORD=secret

#Change the port for accessing site (Defaults to 8080)
#Eg: 80

SITE_PORT=8080

#Change the port for PhpMyAdmin (To access DB)
#Eg: 8000

MYADMIN_PORT=8081
```

## .gitignore file

A default `.gitignore` file is supplied for ignoring database if rquired. Laravel `app` folder will contain the normal `.gitignore` provided by Laravel.

## How to add a new composer package?

You may add the package in `composer.json`. And restart the containers.

```
docker-compose restart
```

Or just start the composer

```
docker-compose run composer
```

This will run the composer update and install commands.

## How to run artisan commands?

You will need to use the `exec` command to access artisan.

```
docker-compose exec php-apache artisan <command>
```

## Stopping containers

```
docker-compose down
```

## Issues with MySQL 8

Since version 8, the default MySQL authentication plugin has been changed and may cause problems with Laravel or PHPMyAdmin.

Please see https://mysqlserverteam.com/upgrading-to-mysql-8-0-default-authentication-plugin-considerations/

Easiest Solution is to use MySQL version 5.7.x
