# Getting started with Jenkins

## We will use Docker to run the Jenkins server
## The instructions are for macOS only. Might be suitable for linux as well (unix systems)

## Installation
### Create a network first. Here, we are creating a network named 'jenkins'
```
docker network create jenkins
```

### Pull the Jenkins image, build container with it and run the container
```
docker run -d -p 8080:8080 -p 50000:50000 --network jenkins -v jenkins_volume:/var/jenkins_home --name my_jenkins jenkins/jenkins
# IF we want to pull any specific version of jenkins image, use tag to pull it. For example, jenkins/jenkins:jdk17
```
**This command will pull the latest Jenkins image from docke hub and build a container with it and run it**

### Connect and interact with Jenkins UI
```
http://localhost:8080
```

## Build and run a alpine/socat container to forward traffic from Jenkins to Docker Desktop on Host Machine
**We do this to use Docker of the host machine as a cloud agent. This container will allow Jenkins to use the host machine docker as a docker agent and build container to execute jobs**

### Installation reference
https://stackoverflow.com/questions/47709208/how-to-find-docker-host-uri-to-be-used-in-jenkins-docker-plugin

### Build and run the alpine/socal container
```
docker run -d --restart=always -p 127.0.0.1:2376:2375 --network jenkins -v /var/run/docker.sock:/var/run/docker.sock alpine/socat tcp-listen:2375,fork,reuseaddr unix-connect:/var/run/docker.sock
```
**Now, after the container is up, we can inspect the container, get the IP address and use it as the docker agent URI**
```
tcp://<alpine-socal-container-ip>:2375
```

### While creating agent templates for the docker agent, we can use the image created for python agent
```
docker pull sadmanmadman/myjenkinsagents:python
```
### Or in the image field in the UI, we can just provide the image name and Jenkins will pull and build the python agent with it itself
```
sadmanmadman/myjenkinsagents:python
```
### Now, the Jenkins docker agent is ready to execute jobs

# Some references that I have used and could be helpful
- https://youtu.be/6YZvp2GwT0A?si=79FBtXmvulzD3qgD
- https://github.com/devopsjourney1/jenkins-101
- https://aws.plainenglish.io/jenkins-ci-cd-pipeline-explained-by-a-junior-devops-engineer-1d67ecc08a7e
- https://stackoverflow.com/questions/47709208/how-to-find-docker-host-uri-to-be-used-in-jenkins-docker-plugin
