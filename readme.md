# Getting started with Jenkins

# Installation
## We will use Docker to run the Jenkins server.
## The instructions are for MacOS

### Create a network first. Here, we are create a network named 'jenkins'
```
docker network create jenkins
```

### Pull the Jenkins image, build container with it and run the container
```
docker run -d -p 8080:8080 -p 50000:50000 --network jenkins -v jenkins_volume:/var/jenkins_home --name my_jenkins jenkins/jenkins
# IF we want to pull any specific version of jenkins image, use tag to pull it. For example, jenkins/jenkins:jdk17
```
**This command will pull the latest Jenkins image from docke hub and build a container with it and run it.**


### Connect and interact with Jenkins UI
```
http://localhost:8080
```

## Build and run a alpine/socat container to forward traffic from Jenkins to Docker Desktop on Host Machine
**We do this to use Docker of the host machine as a cloud agent. This container will allow Jenkins to use the host machine docker as a docker agent and build container to execute jobs**

### Build and run the alpine/socal container
```
docker run -d --restart=always -p 127.0.0.1:2376:2375 --network jenkins -v /var/run/docker.sock:/var/run/docker.sock alpine/socat tcp-listen:2375,fork,reuseaddr unix-connect:/var/run/docker.sock
```

