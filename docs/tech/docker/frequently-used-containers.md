# Docker 懒人命令集

## 数据库类

### MySQL

```dockerfile
docker run -p 3306:3306 --name mysql -e MYSQL_ROOT_PASSWORD=123456 -e MYSQL_ROOT_HOST=% -d mysql/mysql-server:latest
```

### PostgreSQL

```dockerfile
docker run -p 5432:5432 --name sandbox_postgres -e POSTGRES_PASSWORD=123456 -d postgres
```

### MongoDB

```dockerfile
docker run -itd --name sandbox_mongo -p 27017:27017 mongo --auth
```

[Docker 安装 MongoDB](https://www.runoob.com/docker/docker-install-mongodb.html)

### SQL server

```dockerfile
docker run -e "ACCEPT_EULA=Y" -e "SA_PASSWORD=Nice@Passw0rd" \
   -p 1433:1433 --name docker_sqlserver -h docker_sqlserver \
   -d \
   mcr.microsoft.com/mssql/server:2017-latest
```

Username: SA passwd: Nice@Passw0rd

[Docker: Install containers for SQL Server on Linux - SQL Server | Microsoft Docs](https://docs.microsoft.com/en-us/sql/linux/quickstart-install-connect-docker?view=sql-server-2017&preserve-view=true&pivots=cs1-bash)

### Oracle

version: oracle-11g

```dockerfile
docker volume create oracle-11g
docker run -d -p 1521:1521 --name oracle-11g -e ORACLE_ALLOW_REMOTE=true -v oracle-11g:/u01/app/oracle wnameless/oracle-xe-11g-r2
```

login credentials:

```text
hostname: localhost
port: 49161
sid: xe
username: system
password: oracle
```

ref: [GitHub - wnameless/docker-oracle-xe-11g: Dockerfile of Oracle Database Express Edition 11g Release 2](https://github.com/wnameless/docker-oracle-xe-11g)

## web 环境

### Apache2+PHP

```dockerfile
docker run -p 80:80 --name a2php -v "$PWD":/var/www/html -d thecodingmachine/php:7.4-v3-apache
```

[thecodingmachine/docker-images-php: A set of PHP Docker images](https://github.com/thecodingmachine/docker-images-php)

### LNMP + Redis

更适合中国宝宝体质的 LNMP 环境

[PHP 本地开发环境 Docker-测试版](https://github.com/zhangjunjie6b/phpdocker)
