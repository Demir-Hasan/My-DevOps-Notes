## Installing Jenkins
There are 2 ways:
- Intalling directly on the OS
- Pulling Jenkins image and run as a container

### Running Jenkins as a Docker Container
Once we get the docker installed in our local/remote server, we use the following command to run Jenkins container:

`docker run -p 8080:8080 -p 50000:50000 -d -v jenkins_home:/var/jenkins_home **jenkins/jenkins:lts**`

Note that the name of the docker image is: jenkins/jenkins

Then check if the container is running, `docker ps`

If you run docker container on local machine, open a browser and go to `https://localhost:8080`

If you run docker container on remote server, open a browser and go to `IP address:8080`

You will need the password to login the page: 

`docker exec -ti [image ID] bash`
`cat /var/jenkins_home/secrets/initialAdminPassword`

The password is also stored at: 

`docker volume inspect jenkins_home` `ls mountpoint` `cat`

## Installing Tools

There are 2 ways to install tools on Jenkins

1. Jenkins plugins: You can install a plugin on User Interface
2. On server : If you run Jenkins as a container, you need to install the tool inside the container while container is running. (root user)

`docker exec -u 0 -ti [docker image ID] bash` `cat /etc/issue` `apt update` ...

## Docker in Jenkins Container

This is simply mounting "docker runtime" directory from host/server into Jenkins continer as a volume. This will made docker availabe inside the Jenkins
continer.

`docker volume ls`

`docker run -p 8080:8080 -p 50000:50000 -d
-v jenkins_home:/var jenkins_home
-v /var/run/docker.sock:/var/docker.sock
-v $(which docker):/usr/bin/docker
jenkins/jenkins:lts`

### Notes:

When we "start build" we can track the job on terminal inside the container.

`docker exec -ti [docker image ID] bash` `ls /var/jenkins_home/job & /var/jenkins_home/workspace`

