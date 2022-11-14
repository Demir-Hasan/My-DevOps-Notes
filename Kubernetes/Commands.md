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
- `echo -n 'username' | base64` it returns the encrypted word of the word in quotes. 
#### Volumes
- storage on local machine or remote outside of the cluster
#### Deployment
- blueprint for pods
- In practice you create depolyments not pods
- abstraction of pods
- It is for stateless apps
- For stateful apps like databases statefulsets are used
- DB are often hosted outside of K8s cluster
- Everything CRUD is at the deployment level. Kubernetes handles the rest of it. 



### Minikube

- One-node cluster
- For test and/or learning purposes
- Master processes and worker processes run on ONE node
- Docker is pre-installed

### Kubectl

- Command line tool for K8s cluster
- Api server is the main entrypoint to the Kubernetes cluster


### Minikube start 

- Go to official web page for the documentation
- Minikube can run either as VM or as continer
- Follow the instruction on the official web page
- `minikube start --driver docker` after installing minikube in the local machine

### Commands

- `minikube status` to check the components run ok.
- `kubectl get node` display all the nodes in the cluster
- `kubectl get pod` display the pods
- `kubectl get pod -o wide`
- `kubectl get deployment [NAME] -o yaml` output as a yaml format  
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
- `kubectl apply -f config-file.yaml` create a deployment from a yaml file. If already created it updates the deployment

### Configuration File
Every config file has 3 parts
- metadata
- specification
- status (automatically added by K8s)

There is a YAML validator online to check the syntax and indentation

#### Connecting Components (Labels & Selectors & Ports)
- To establish connection we use labels and selectors
- Metadata part containes the label
- Spec part contains the selector
```
kind: Deployment
metadata:
  name: nginx-deployment
  labels:
    app: nginx
```

```
kind: Service
metadata:
  name: nginx-service
spec:
  selector:
    app: nginx
  ports:
    - protocls: TCP
      port: 80
      targetPort: 8080 (It should be match the containerPort at the Deployment YAML file)
```

### Namespaces
- You can organize resources in namespaces
- It is like a virtual cluster inside a cluster
- There are 4 default namespaces
- Resource you creare are located in "default" namespaces
- `kubectl create namespace [my-namespaca]`
- You can create the namespace in the ConfigMap under metadate (preferred way)
```
kind: ConfigMap
metadata:
  name: mysql-configmap
  namespace: my-namespace
```  
- Why namespace?
- Grouping namespaces into for example one for Database, one for Monitoring, one for Elastic Stack, and one for Nginx-Ingress
- Differnt teams better use different namespaces (it help avoiding conflicts, overwriting)
- Access and Resouce Limits on Namespaces
- Limit CPU, RAM, Storage per namespace
- You can't access most resources from another Namespace
- there is a way to access to connect a resource from a different namespace
- Creating a component in a namespace : `kubectl apply -f mysql-configmap.yaml --namespace=my-namespace` otherwise it creates the component in default namespace
- `kubens` (kubenamespace) list all the namespaces and highlight the active one
- `kubens [my-namespace]` changes active namespace to my-namepace. After changing to my-namesapce we can type commands without providing the namespace

### Services
- Each Pod has its own IP address but it is ephemeral so we use service which provide stable IP address. It also provide loadbalancing. they are good at loose coupling 
- Service establish communication with pods via selectors, and ports in the YAML file. (In the deployment YAML file the pods have labels)
- When you create a service, K8s creates an Enpoint object which has same name as Service. So you can keep track of which Pods are the members/endpoints of the Service
- Service Port is arbitrary but targetPort must match the port the continer is listening at.
- 
- There are different types of services
- ClusterIP Services: (Internal Service) For example, if you have 3 worker nodes in the cluster, each node have a range of ip addresses. node1(10.2.1.x), node2(10.2.2.x), node3(10.2.3.x) `kubectl get pod -o wide` you can see the details of the pods in detail.
- Headless Services: )In the YAML file under spec set the clusterIP as "none")Client wants to communicate with 1 specific Pod directly or Pods want to talk directly with specific Pod without going to ClusterIP Service first which directs the request to a random Pod. In this case client needs to figure out IP addresses of each Pod. It is done by DNS Lookup. Headless service is used for stateful components like DBs.
- NodePort Services: (External Service) Can have access directly from outside. nodePort attribute under ports section of the YAML file has a range between 30000 and 32767
- LoadBalancer Services: becomes accessible externally through cloud providers LoadBalancer

### Nginx-deployment YAML file

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

