MariaDB plugin for Docker
------------------------

Easy creation of a MariaDB docker container with a persistent database.

A quick hack based on https://github.com/Kloadut/dokku-md-plugin. Adapted for use locally on OSX without dokku.

Installation
------------
```
git clone https://github.com/neam/docker-md-plugin
./docker-md-plugin/install
```


Commands
--------
```
$ ./docker-md-plugin/commands help
     mariadb:create <app>      Create a MariaDB container
     mariadb:delete <app>      Delete specified MariaDB container
     mariadb:info <app>        Display database informations
     mariadb:link <app> <db>   Link an app to a MariaDB database
     mariadb:console <app>     Open mysql-console to MariaDB container
     mariadb:dump <app> <file> Dump default db database into file <file> is optional. 
     mariadb:logs <app>        Display last logs from MariaDB container
```

Info
--------
This plugin populates the following envvars for you to use in your docker container:

* DATABASE_URL
* DB_HOST
* DB_PORT
* DB_NAME
* DB_USER
* DB_PASSWORD

Simple usage
------------

Create a new DB:
```
$ ./docker-md-plugin/commands mariadb:create foo

-----> MariaDB container created: mariadb/foo

       Host: 172.16.0.104
       User: 'root'
       Password: 'RDSBYlUrOYMtndKb'
       Database: 'db'
       Public port: 49187
```

Advanced usage
--------------

Inititalize the database with SQL statements:
```
cat init.sql | dokku mariadb:create foo
```

Deleting databases:
```
./docker-md-plugin/commands mariadb:delete foo
```

Linking an app to a specific database:
```
./docker-md-plugin/commands mariadb:link foo bar
```

MariaDB logs (per database):
```
./docker-md-plugin/commands mariadb:logs foo
```

Database informations:
```
./docker-md-plugin/commands mariadb:info foo
```

Login to mariadb console
```
./docker-md-plugin/commands mariadb:console
```

Import to existing database
```
./docker-md-plugin/commands mariadb:console < import.sql
```
