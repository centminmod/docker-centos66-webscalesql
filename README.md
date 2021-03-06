[WebScaleSQL MySQL Server](http://webscalesql.org/) on CentOS 6.7 64bit Docker container build intended for use with [CentminMod.com LEMP stack](http://centminmod.com). 

### My Docker Hub repo

* https://registry.hub.docker.com/u/centminmod/docker-centos66-webscalesql/

### Centmin Mod Docker Development forums

* https://community.centminmod.com/forums/centmin-mod-docker-development.52/

---
### Default MySQL root user password 

* The default MySQL root user password is set to = mysqlpass with added replication user = repl

#### Grab from Docker Hub

    docker pull centminmod/docker-centos66-webscalesql

Run docker container

    docker run -d -p 3306:3306 -t centminmod/docker-centos66-webscalesql

or specify a name e.g. webscale1

    docker run --name webscale1 -d -p 3306:3306 -t centminmod/docker-centos66-webscalesql

or if host system already has MySQL running on port 3306 need to map to another local host port e.g. 3307

    docker run --name webscale1 -d -p 3307:3306 -t centminmod/docker-centos66-webscalesql

to access container via bash if started with name = webscale1

    docker exec -ti webscale1 /bin/bash

to connect from host system to MariaDB docker container use the -h IP address which is shown for the docker0 network interface

    ifconfig docker0 | grep 'inet '
    inet addr:172.17.42.1  Bcast:0.0.0.0  Mask:255.255.0.0

or connect via IP derived from docker inspect command for container named webscale1

    docker inspect --format '{{ .NetworkSettings.IPAddress }}' webscale1
    172.17.0.2    

e.g. host system running CentminMod.com LEMP stack MariaDB 10 server hence the client is 10.0.16 to connect to WebScaleSQL 5.6.23 docker container

    mysqladmin -P 3307 -h 172.17.42.1 -u root -p ver                   
    Enter password: 
    mysqladmin  Ver 9.1 Distrib 10.0.16-MariaDB, for Linux on x86_64
    Copyright (c) 2000, 2014, Oracle, MariaDB Corporation Ab and others.
    
    Server version          5.6.23
    Protocol version        10
    Connection              172.17.42.1 via TCP/IP
    TCP port                3307
    Uptime:                 5 sec
    
    Threads: 1  Questions: 2  Slow queries: 0  Opens: 15  Flush tables: 1  Open tables: 8  Queries per second avg: 0.400

---

#### Building from Dockerfile

Grab files

    git clone https://github.com/centminmod/docker-centos66-webscalesql.git

Build docker container with image name = centos66-webscalesql. Run command within same directory as Dockerfile

    docker build -t centos66-webscalesql .

To run follow same run steps above.

