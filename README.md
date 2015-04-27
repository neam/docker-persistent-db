Persistent DB helper for Docker
------------------------

Easy creation of a MySQL docker container with persistent data. 

A quick hack based on https://github.com/Kloadut/dokku-md-plugin. Adapted for use locally on OSX without dokku.

Installation
------------

Run the following from your project directory:

```
git clone https://github.com/neam/docker-persistent-db --recursive ../docker-persistent-db/
../docker-persistent-db/install
```

Then, create a persistent database according to "Simple usage" below.

The metadata about the database containers is stored on the docker host in the `../docker-persistent-db/.db/` directory.

Commands
--------

Note: Currently only the `db:create` command is verified to work.

```
$ ../docker-persistent-db/commands help
     db:create <app>      Create a db container
     db:delete <app>      Delete specified db container
     db:info <app>        Display database informations
     db:link <app> <db>   Link an app to a db database
     db:console <app>     Open mysql-console to db container
     db:dump <app> <file> Dump default db database into file <file> is optional. 
     db:logs <app>        Display last logs from db container
```

Simple usage
------------

Create a new DB:
```
$ ../docker-persistent-db/commands db:create foo

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
../docker-persistent-db/commands db:delete foo
```

Linking an app to a specific database:
```
../docker-persistent-db/commands db:link foo bar
```

db logs (per database):
```
../docker-persistent-db/commands db:logs foo
```

Database information:
```
../docker-persistent-db/commands db:info foo
```

Login to db console
```
../docker-persistent-db/commands db:console
```

Import to existing database
```
../docker-persistent-db/commands db:console < import.sql
```
