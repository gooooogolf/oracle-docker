# oracle-docker
Setup Oracle Database Server with Docker

### Prerequsite ###

* [Docker](https://store.docker.com/ "Get started with Docker")
* [SQL Developer command line](http://www.oracle.com/technetwork/developer-tools/sqlcl/overview/index.html "SQL Developer command line")

### Setup ###

1. Pull image from docker store
```
$ docker pull store/oracle/database-enterprise:12.2.0.1-slim
$ docker images
REPOSITORY                         TAG                 IMAGE ID            CREATED             SIZE
store/oracle/database-enterprise   12.2.0.1-slim       27c9559d36ec        12 months ago       2.08GB
```

2. Create docker container
```
$ docker run -d -it --name oracle -p 32122:1521 store/oracle/database-enterprise:12.2.0.1-slim
0d758fca613973c5d9c3043d06922ac8a4f7c57d5d88aec6bb468b6910d1f99e
$ docker ps
CONTAINER ID        IMAGE                                            COMMAND                  CREATED             STATUS                            PORTS                               NAMES
0d758fca6139        store/oracle/database-enterprise:12.2.0.1-slim   "/bin/sh -c '/bin/ba…"   6 seconds ago       Up 5 seconds (health: starting)   5500/tcp, 0.0.0.0:32122->1521/tcp   oracle

# For all the examples below the name "oracle" was used.
# You can use any name you want or just use the docker container ID to reference it
```
Container | Container Port | Local Port |Description
--- | --- | ---|---
oracle | 1521 | 32122 | TNS listener for Oracle 12.2

3. Check oracle status is up
```
$ docker ps
CONTAINER ID        IMAGE                                            COMMAND                  CREATED             STATUS                   PORTS                               NAMES
0d758fca6139        store/oracle/database-enterprise:12.2.0.1-slim   "/bin/sh -c '/bin/ba…"   2 minutes ago       Up 2 minutes (healthy)   5500/tcp, 0.0.0.0:32122->1521/tcp   oracle

# Look in the STATUS column for the container. During "boot" time it will say "... (health: starting)".
# Wait until it says (healthy) before trying anything else.
```

4. Connecting from within the container
```
$ docker exec -it oracle bash -c "source /home/oracle/.bashrc; sqlplus /nolog"

SQL*Plus: Release 12.2.0.1.0 Production on Sun Aug 19 10:17:06 2018

Copyright (c) 1982, 2016, Oracle.  All rights reserved.

SQL> 
```

5. Setup sqlcl for connect oracle database server
```
cd ~/Downloads

#Assuming you already have an /opt/oracle directory (I had one for the instant client)
cp -r sqlcl /opt/oracle

#Give sqlcl execute permission
cd /oracle/sqlcl/bin
chmod 755 sql

#Add directory to path so can run anywhere in the command line:
$ vi ~/.bash_profile 
export SQLCL_HOME="/opt/oracle/sqlcl"
export PATH="$SQLCL_HOME/bin:$PATH"

```

6. Connecting from outside the container
```
# To connect to the CDB
$ sql sys/Oradoc_db1@localhost:32122:orclcdb as sysdba

SQLcl: Release 18.2 Production on Sun Aug 19 17:30:34 2018

Copyright (c) 1982, 2018, Oracle.  All rights reserved.

Connected to:
Oracle Database 12c Enterprise Edition Release 12.2.0.1.0 - 64bit Production


SQL> 

```

