Persistent DB helper for Docker
------------------------

Easy creation of a MySQL/MariaDB docker container with a persistent database.

A quick hack based on https://github.com/Kloadut/dokku-md-plugin. Adapted for use locally on OSX without dokku.

Installation
------------
```
git clone https://github.com/neam/docker-md-plugin --recursive
./docker-md-plugin/install
```


Commands
--------
```
$ ./docker-md-plugin/commands help
     db:create <app>      Create a db container
     db:delete <app>      Delete specified db container
     db:info <app>        Display database informations
     db:link <app> <db>   Link an app to a db database
     db:console <app>     Open mysql-console to db container
     db:dump <app> <file> Dump default db database into file <file> is optional. 
     db:logs <app>        Display last logs from db container
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
$ ./docker-md-plugin/commands db:create foo

-----> db container created: db/foo

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
cat init.sql | dokku db:create foo
```

Deleting databases:
```
./docker-md-plugin/commands db:delete foo
```

Linking an app to a specific database:
```
./docker-md-plugin/commands db:link foo bar
```

db logs (per database):
```
./docker-md-plugin/commands db:logs foo
```

Database informations:
```
./docker-md-plugin/commands db:info foo
```

Login to db console
```
./docker-md-plugin/commands db:console
```

Import to existing database
```
./docker-md-plugin/commands db:console < import.sql
```
