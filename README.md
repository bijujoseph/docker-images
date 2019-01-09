
This repository contains **Dockerfile** used primarily during Jenkins builds.



## Useful commands for building
```
cd jenkins
docker build -t bijujoseph/jenkins:0.8 .
docker push bijujoseph/jenkins:0.8
docker tag bijujoseph/jenkins:0.8  bijujoseph/jenkins:latest
docker push bijujoseph/jenkins:latest


cd jenkins-slave-server
docker build -t bijujoseph/jenkins-slave-client:0.25 .
docker push bijujoseph/jenkins-slave-client:0.25
docker tag bijujoseph/jenkins-slave-client:0.25 bijujoseph/jenkins-slave-client:latest
docker push bijujoseph/jenkins-slave-client:latest

cd pg-node
docker build -t bijujoseph/pg-node:0.0.2 .
docker push bijujoseph/pg-node:0.0.2
docker tag bijujoseph/pg-node:0.0.2 bijujoseph/pg-node:latest
docker push bijujoseph/pg-node:latest

docker run -e POSTGRES_PASSWORD=qpp -e POSTGRES_USER=qpp -e POSTGRES_DB=qpp bijujoseph/pg-node

cd mysql-node
docker build -t bijujoseph/mysql-node:0.0.2 .
docker tag bijujoseph/mysql-node:0.0.2 bijujoseph/mysql-node:latest
docker push bijujoseph/mysql-node:latest
docker push bijujoseph/mysql-node:0.0.2

cd scala-sbt
docker build -t bijujoseph/scala-sbt:0.0.1 .
docker tag bijujoseph/scala-sbt:0.0.1 bijujoseph/scala-sbt:latest
docker push  bijujoseph/scala-sbt:0.0.1
docker push bijujoseph/scala-sbt:latest

```




## Contribution policy ##

Contributions via GitHub pull requests are gladly accepted from their original author. Along with any pull requests, please state that the contribution is your original work and that you license the work to the project under the project's open source license. Whether or not you state this explicitly, by submitting any copyrighted material via pull request, email, or other means you agree to license the material under the project's open source license and warrant that you have the legal authority to do so.


## License ##

This code is open source software licensed under the [Apache 2.0 License]("http://www.apache.org/licenses/LICENSE-2.0.html").