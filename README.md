ActiveMQ Artemis
================
This docker file is based on Apache ActiveMQ Artemis Ubuntu docker file. 
Instead of using binaries form build, this one downloads official release 
build archive file.

Usage of docker image is same as documented in original README at:
https://github.com/apache/activemq-artemis/tree/main/artemis-docker

Docker file is derived from Ubuntu docker file at:
https://github.com/apache/activemq-artemis/blob/main/artemis-docker/Dockerfile-adoptopenjdk-11

Build image is published in docker hub repository and may be used without building it:
https://hub.docker.com/repository/docker/frantiseksidak/activemq-artemis

Build
-----
To build docker image from docker file run this command in folder containing docker file:
```
docker build -f ./Dockerfile -t activemq-artemis .
```

Run
---
To create and run container from image run this command:
```
docker run --rm -d -p 1883:1883/tcp -p 5445:5445/tcp -p 5672:5672/tcp -p 61613:61613/tcp \
    -p 61616:61616/tcp -p 8161:8161/tcp -p 9404:9404/tcp apache-artemis:latest
```
or this, for image from docker hub repository:
```
docker run --rm -d -p 1883:1883/tcp -p 5445:5445/tcp -p 5672:5672/tcp -p 61613:61613/tcp \
    -p 61616:61616/tcp -p 8161:8161/tcp -p 9404:9404/tcp frantiseksidak/activemq-artemis:latest
```

Compose
-------
You can use built image as part of docker-compose solution yaml file:
```
version: '3.4'

services:
  artemis:
    container_name: artemis
    image: frantiseksidak/activemq-artemis
    ports:
      - 8161:8161 # Web Server
      - 9404:9404 # JMX Exporter
      - 61616:61616 # Port for CORE,MQTT,AMQP,HORNETQ,STOMP,OPENWIRE
      - 5445:5445 # Port for HORNETQ,STOMP
      - 5672:5672 # AMQP
      - 1883:1883 # MQTT
      - 61613:61613 #Port for STOMP
    volumes:
      - ./data/activemq-artemis:/var/lib/artemis-instance
```
