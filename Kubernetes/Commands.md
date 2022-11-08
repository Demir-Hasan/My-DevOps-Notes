### Orchestration Tools Offer
- High availability : No downtime
- Scalability : High performance
- Disaster Recovery : backup and restore

### Main Kubernetes Components 
#### Nodes
- each nodes has multiple pods on it
- 3 processes must be installed on every node: container runtime, Kubelet (it interacts with both the container and the node, it starts the pod with a container inside), Kube Proxy (forwards requests)   
- Worker nodes do actual work

#### Master Nodes
- API server
- Scheduler
- Controller Manager
- etcd (key-value store, cluster changes are stored here) 


#### Pod 
- smallest unit
- abstraction over container
- only interact with this layer
- usually 1 app per pod
- each pod gets its own IP address
#### Service 
- pod communicate with each other using service
- permanant IP address
- Load Balancer
- external service
#### Ingress
- internal service 
#### ConfigMap
- setting the properties of the apps in the nodes
- external config of your application
- if you change sth you just adjust the configmap
- dont put credentials in the config map 
#### Secret
- used to store secret date
- base64 encoded
- store things like credentials
- as env variables
#### Volumes
- storage on local machine or remote outside of the cluster
#### Deployment
- blueprint for pods
- In practice you create depolyments not pods
- abstraction of pods
- It is for stateless apps
- For stateful apps like databases statefulsets are used
- DB are often hosted outside of K8s cluster



### Minikube

- One-node cluster
- For test and/or learning purposes
- Master processes and node processes run on ONE machine
- Docker is pre-installed

### Kubectl

- Command line tool for K8s cluster
- Api server is the main entrypoint to the Kubernetes cluster


### Minikube start 

- Go to official web page for the documentation
- Minikube can run either as VM or as continer
- Follow the instruction on the official web page

### Commands

- `minikube status` to check the components run ok.
- `kubectl get node` display all the nodes in the cluster
- `kubectl get pod` display the pods
- `kubectl get services`
- `kubectl create -h` all the things we can create
- `kubectl create deployment mongo-depl --image=mongo`
- `kubectl get deployment`
- `kubectl get replicaset`
- `kubectl edit deployment NAME`
- `kubectl logs`
- `kubectl describe pod NAME`
- `kubectl exec -ti NAME -- bin/bash` 
- `kubectl delete deployment NAME`
- `kubectl apply -f config-file.yaml`

```
apiVersion: apps/v1
kind: Deployment
metadata:
  name: nginx-deployment
spec:
  selector:
    matchLabels:
      app: nginx
  replicas: 2 # tells deployment to run 2 pods matching the template
  template:
    metadata:
      labels:
        app: nginx
    spec:
      containers:
      - name: nginx
        image: nginx:1.14.2
        ports:
        - containerPort: 80
```

