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

```
docker run -p 8080:8080 -p 50000:50000 -d
-v jenkins_home:/var/jenkins_home (re-attaching the old jenkins container data)
-v /var/run/docker.sock:/var/docker.sock
-v $(which docker):/usr/bin/docker (makes docker available inside jenkins container)
jenkins/jenkins:lts
```

### Notes:

When we "start build" we can track the job on terminal inside the container.

`docker exec -ti [docker image ID] bash` `ls /var/jenkins_home/job & /var/jenkins_home/workspace`

### Connecting Jenkins to Github (web-hook)

- On Jenkins UI, after we create a new project, at the build trigger section  we select Github hook trigger for GITScm polling.

- Once we created a Jenkinsfile on Github and add the URL on Jenkins, we copy the Jenkins URL to our clipboard and paste it on GitHub - Settings - Webhooks  Payload URL. The end of the URL shoul be as : `....com/github-webhook/` Then the following selector shoul be set as content type: application/json. After adding a web hook github ping the Jenkins and then when we refresh the page we will see a green check mark. 

- To give it a try we can add a text on Readme.md file. After we commit the changes, jenkins will be triggered automatically.

### Jenkins Roles

- Jenkins Administrator: Manages Jenkins, sets up Jenkins Cluster, Installs plugins, Backs up Jenkins data
- Jenkins User: Creating the actual jobs to run workflows

### Jenkins Tools, Plugins

- Depending on the App (programing language) you need to have different tools installed and configured on Jenkins. (NPM for JS apps, Maven for Java apps)
- So, there are 2 ways to have these tools: One is to install it as a plugin, other is installing it on the server directly (if jenkins running as a container).
1) to login the Jenkins container as a root user `docker exec -u 0 -ti {container ID} bash`).
2) `apt update`
3) `apt install curl`
4) `curl -sL https://deb.nodesource.com/setup_10.x -o nodesource_setup.sh`
5) `ls`
6) `bash nodesource_setup.sh`
7) `apt install node.js`  

