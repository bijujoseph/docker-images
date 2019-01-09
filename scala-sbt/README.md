# Scala and sbt Dockerfile

This repository contains **Dockerfile** of [Scala](http://www.scala-lang.org) and [sbt](http://www.scala-sbt.org).


## Base Docker Image ##

* [openjdk](https://hub.docker.com/_/openjdk)


## Installation ##

1. Install [Docker](https://www.docker.com)
2. Pull [automated build](https://hub.docker.com/r/bijujoseph/scala-sbt) from public [Docker Hub Registry](https://registry.hub.docker.com):
```
docker pull bijujoseph/scala-sbt:latest
```
Alternatively, you can build an image from Dockerfile available at [Git Repo](https://github.com/bijujoseph/docker-images)
```
cd scala-sbt
docker build -t bijujoseph/scala-sbt:0.0.1 .
docker tag bijujoseph/scala-sbt:0.0.1 bijujoseph/scala-sbt:latest
```


## Usage ##

```
docker run -it --rm hbijujoseph/scala-sbt
```
