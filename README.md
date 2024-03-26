# Kubernetes Hands-On - Deploy Microservices to the AWS Cloud

[Udemy Course](https://www.udemy.com/course/kubernetes-microservices/?couponCode=KEEPLEARNING)

[Course Docker Images](https://hub.docker.com/search?q=richardchesterwood)

[Course Github Repo for the Docker Images](https://github.com/DickChesterwood/k8s-fleetman)

## Dockerhub images

Intel/AMD user will be using an image from Dockerhub like this:

image: richardchesterwood/k8s-fleetman-webapp-angular:release1

```powershell
docker container run -d -e "SPRING_PROFILES_ACTIVE=local-microservice" --name fleetman-webapp --network fleetman -p 8080:80 richardchesterwood/k8s-fleetman-webapp-angular:release1
```

```powershell
kubectl version

kubectl get all


```
