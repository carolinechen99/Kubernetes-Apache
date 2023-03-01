# Kubernetes-Apache
This is a simple Apache web server deployment using minikube. 

## Prerequisites
* [Minikube](https://kubernetes.io/docs/tasks/tools/install-minikube/)
* [Kubectl](https://kubernetes.io/docs/tasks/tools/install-kubectl/)
* [Docker](https://docs.docker.com/install/)

## Configuration
1. Configure environment to use minikube’s Docker daemon
```bash
$ eval $(minikube docker-env)
```
2. Set up a local Docker registry
```bash
$ docker run -d -p 5000:5000 --restart=always --name registry registry:2
```

## Docker Image
1. Build the Docker image
```bash
$ docker build -t cat:1.0.0 .
```
2. Tag the image
```bash
docker tag cat localhost:5000/cat:1.0.0
```

## Deployment with K8s
1. Apply the deployment
```bash 
$ kubectl apply -f deployment.yaml
```
2. Apply the service
```bash
$ kubectl apply -f service.yaml
```
3. Get the service URL
```bash
$ minikube service cat --url
```
4. Open the URL in a browser

## Cleanup
1. Delete the deployment
```bash
$ kubectl delete -f deployment.yaml
```
2. Delete the service
```bash
$ kubectl delete -f service.yaml
```
3. Delete the Docker image
```bash
$ docker rmi localhost:5000/cat:1.0.0
```
4. Delete the Docker registry
```bash
$ docker rm -f registry
```
5. Stop the minikube cluster
```bash
$ minikube stop
```

### References:
* [DOCKER & KUBERNETES](https://www.bogotobogo.com/DevOps/Docker/Docker_Kubernetes_Minikube.php)
* [Cat Island Wiki](https://en.wikipedia.org/wiki/Cat_Island)