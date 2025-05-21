# Getting started with Jenkins

# Installation
## We will use Docker to run the Jenkins server
```
docker run -d -p 8080:8080 -p 50000:50000 --network jenkins -v jenkins_volume:/var/jenkins_home --name my_jenkins jenkins/jenkins
# IF we want to pull any specific version of jenkins image, use tag to pull it
```
*** This command will pull the latest Jenkins image from docke hub and build a container with it and run it. ***



