# Kubernetes Hands-On - Deploy Microservices to the AWS Cloud

[Udemy Course](https://www.udemy.com/course/kubernetes-microservices/?couponCode=KEEPLEARNING)

[Course Docker Images](https://hub.docker.com/u/richardchesterwood)

[Course Github Repo for the Docker Images](https://github.com/DickChesterwood/k8s-fleetman)

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

### 5

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

### 6

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

Open browser: http://localhost:30080/
