### What is a container?
- Operation System has two layers (1. Kernel (which communicate with hardware) 2. Application Layer)
- Docker virtualize application layer of the OS. It uses the kernel of the host. Virtual Machine on the other hand has its own Kernel. It virtualize the complete OS.
- Docker images are much smaller in size cople of MB (VMs are couple of GB)
- Images are very fast
- Portable: Easily shared and moved
- packaged app with all necessary dependencies and configs
- you can run 2 different version of one app without experiencing any conflict
- most of the time Linux based image is used because of its small size OS (alpine:3.10)
- Public repositories don't require login and authentication
- Containers are made up of layers, so when a newer version of an app is downloaded, only newer layers get to be downloaded.
- image (not running) / container (running)

```
When you install Docker Engine you will have below:
1. Server (pulling images, managing images&containers) is responsible for:
  a. Container Runtime (pulling images, managing container lifecycle)
  b. Volumes (persisting data)
  c. Network (container comunication)
  d. Build Image (building own docker images)
2. API (interacting with Docker server)
3. CLI (Client to execute Docker Commands)
```

- If you only need a container runtime there are options like containerd and cri-o
- If you only need a container builder you may consider buildah


### Docker Commands
- `docker pull` pulls an image from a public repo
- `docker images` list the images that are hosted locally  
- `docker run {image name:tag}` runs a container
- `docker ps` lists running containers
- `Ctrl + C` forces to stop a running container
- `docker run -d {image name}` -d means start a container in a detached mode
- `docker stop {contianer ID}`
- `docker start {container ID}`
- `docker ps -a` shows all the containers that are running and not running
- `docker run -p6000:6379 {image name}` Host Port : 6000, Container Port: 6379. Different continers may have the same port number but they have to connect different ports of the host
- ``
- ``
- ``
- 
