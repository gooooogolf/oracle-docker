# oracle-docker
Setup Oracle Database Server with Docker

### Prerequsite ###
* Install [Docker](https://store.docker.com/ "Get started with Docker")
* [SQL Developer command line](http://www.oracle.com/technetwork/developer-tools/sqlcl/overview/index.html "SQL Developer command line")

### 1. Pull image from docker store ###
```
$ docker pull store/oracle/database-enterprise:12.2.0.1-slim
$ docker images
REPOSITORY                         TAG                 IMAGE ID            CREATED             SIZE
store/oracle/database-enterprise   12.2.0.1-slim       27c9559d36ec        12 months ago       2.08GB
```
