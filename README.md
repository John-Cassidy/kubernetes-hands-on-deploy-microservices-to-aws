# Kubernetes Hands-On - Deploy Microservices to the AWS Cloud

[Udemy Course](https://www.udemy.com/course/kubernetes-microservices/?couponCode=KEEPLEARNING)

[Course Docker Images](https://hub.docker.com/u/richardchesterwood)

[Course Github Repo for the Docker Images](https://github.com/DickChesterwood/k8s-fleetman)

![Microservices Design](./resources/01-microservices-design.png)

## Dockerhub images

Intel/AMD user will be using an image from Dockerhub like this:

image: richardchesterwood/k8s-fleetman-webapp-angular:release1

```powershell
docker container run -d -e "SPRING_PROFILES_ACTIVE=local-microservice" --name fleetman-webapp --network fleetman -p 8080:80 richardchesterwood/k8s-fleetman-webapp-angular:release1
```

## Kubernetes Documentation

[Docs Reference](https://kubernetes.io/docs/reference/)

[Kubernetes API](https://kubernetes.io/docs/reference/kubernetes-api/)

[API Reference](https://kubernetes.io/docs/reference/generated/kubernetes-api/v1.29/)

```powershell
kubectl version

kubectl get all

kubectl cluster-info

kubectl get services
NAME            TYPE        CLUSTER-IP   EXTERNAL-IP   PORT(S)   AGE
kubernetes      ClusterIP   10.96.0.1    <none>        443/TCP   7h8m
[ServiceName]   [NodePort]  ???          ???           ???       ???
kubectl get service [ServiceName]

```

## Chapters

### 5 Pod

```powershell
# create pod
cd '.\course-resources\Chapter 5 Pods'
kubectl apply -f first-pod.yaml
pod/webapp created
# delete pod
kubectl delete -f first-pod.yaml

kubectl get pods

kubectl describe pod webapp

kubectl exec webapp ls

# connect to pod
kubectl -it exec webapp sh
# list folders
ls
# download index.html
wget http://localhost
Connecting to localhost (127.0.0.1:80)
index.html           100%
# read index.html
cat index.html

# If you are using the Kubernetes that ships with Docker Desktop,
# then you just use "localhost" or "127.0.0.1" as the address.
# Don't forget the port number of your NodePort. so "127.0.0.1:30080" should work for the webapp.
# Sometimes with docker desktop , localhost doesn't work and you will need the following command:
kubectl port-forward svc/fleetman-webapp 30080:80

```

### 6 Service

```powershell
# create pod
cd '.\course-resources\Chapter 6 Services'
kubectl apply -f first-pod.yaml
pod/webapp created
# delete pod
kubectl delete -f first-pod.yaml

# create service
kubectl apply -f webapp-service.yaml
service/fleetman-webapp created
# delete service
kubectl delete -f webapp-service.yaml

# describe service
kubectl describe svc fleetman-webapp

# show pod labels
kubectl get pods --show-labels

# show pods filtered by label
kubectl get pods --show-labels -l release=0
```

Kubernetes embedded within Docker Desktop
Open browser: http://localhost:30080/

### 7 ActiveMQ

Kubernetes embedded within Docker Desktop, uses localhost:30080 to access Service for Frontend Pod.

For the ActiveMq queue, we will need to access it on localhost:30010.

If it is not accessible, run the following port-forward command:

```powershell
kubectl port-forward svc/fleetman-queue 30010:8161
```

```powershell
cd '.\course-resources\Chapter 7 Exercise'
# Create
kubectl apply -f .

kubectl get all

Kubernetes embedded within Docker Desktop
WebApp: http://localhost:30080/
Queue: http://localhost:30010/
# username: admin
# password: admin

# Delete
kubectl delete -f .
```

### 8 ReplicaSets

```powershell
cd '.\course-resources\Chapter 8 ReplicaSets'
# Create
kubectl apply -f .

kubectl get all

Kubernetes embedded within Docker Desktop
WebApp: http://localhost:30080/
Queue: http://localhost:30010/
# username: admin
# password: admin

# Delete
kubectl delete -f .
```

### 9 Deployments

```powershell
cd '.\course-resources\Chapter 9 Deployments'
# Create
kubectl apply -f .

kubectl get all

# Modify and redeploy Deployment
kubectl apply -f .
# Check Deployment Rollout Status
kubectl rollout status deployment webapp
# Check Deployment Rollout History
kubectl rollout history deployment webapp

Kubernetes embedded within Docker Desktop
WebApp: http://localhost:30080/
Queue: http://localhost:30010/
# username: admin
# password: admin

# Delete
kubectl delete -f .
```

## 10 Networking and Service Discovery

```powershell
# Namespaces
kubectl get all # default namespace

kubectl get namespaces
NAME              STATUS   AGE
default           Active   164m
kube-node-lease   Active   164m
kube-public       Active   164m
kube-system       Active   164m

kubectl get all -n kube-system


cd '.\course-resources\Chapter 10 Networking'
# Create
kubectl apply -f pods.yaml
kubectl apply -f services.yaml
kubectl apply -f networking-tests.yaml


# Kubernetes embedded within Docker Desktop
# WebApp: http://localhost:30080/
# Queue: http://localhost:30010/
# username: admin
# password: admin

# Delete
kubectl delete -f networking-tests.yaml
kubectl delete -f services.yaml
kubectl delete -f pods.yaml
```

## 11 Microservices

```powershell
kubectl get all

cd '.\course-resources\Chapter 11 Microservices'
# Create
kubectl apply -f .

kubectl describe pod position-tracker-5bdbd5c58-4nkr6
kubectl describe pod api-gateway-77bf7dcbc-kl6xh
kubectl logs -f api-gateway-77bf7dcbc-kl6xh

# Kubernetes embedded within Docker Desktop
# WebApp: http://localhost:30080/
# Queue: http://localhost:30010/
# Tracker on NodePort: http://localhost:30020/vehicles/City Truck
# api-gateway on NodePort: http://localhost:30020
# username: admin
# password: admin

# Delete
kubectl delete -f .
```

## 12 Persistence

```powershell
kubectl get all

cd '.\course-resources\Chapter 12 Persistence'
# Create
kubectl apply -f .

# Kubernetes embedded within Docker Desktop
# WebApp: http://localhost:30080/
# Queue: http://localhost:30010/
# Tracker on NodePort: http://localhost:30020/vehicles/City Truck
# api-gateway on NodePort: http://localhost:30020
# username: admin
# password: admin

# Delete
kubectl delete -f .
```
