# Docker 懒人命令集

## MySQL

```
docker run -p 3306:3306 --name mysql -e MYSQL_ROOT_PASSWORD=123456 -e MYSQL_ROOT_HOST=% -d mysql/mysql-server:latest

```

## PostgreSQL

```
docker run -p 5432:5432 --name sandbox_postgres -e POSTGRES_PASSWORD=123456 -d postgres
```

## MongoDB

```
docker run -itd --name sandbox_mongo -p 27017:27017 mongo --auth
```
[Docker 安装 MongoDB](https://www.runoob.com/docker/docker-install-mongodb.html)

## Apache2+PHP

```
docker run -p 80:80 --name a2php -v "$PWD":/var/www/html -d thecodingmachine/php:7.4-v3-apache
```
[thecodingmachine/docker-images-php: A set of PHP Docker images](https://github.com/thecodingmachine/docker-images-php)

## SQL server

```
docker run -e "ACCEPT_EULA=Y" -e "SA_PASSWORD=Nice@Passw0rd" \
   -p 1433:1433 --name docker_sqlserver -h docker_sqlserver \
   -d \
   mcr.microsoft.com/mssql/server:2017-latest
```

Username: SA passwd: Nice@Passw0rd


[Docker: Install containers for SQL Server on Linux - SQL Server | Microsoft Docs](https://docs.microsoft.com/en-us/sql/linux/quickstart-install-connect-docker?view=sql-server-2017&preserve-view=true&pivots=cs1-bash)