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
- ```

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

