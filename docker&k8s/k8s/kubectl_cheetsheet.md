# Exposing Kubernetes Ports

## Service Types

```
kubectl expose
```

<br/>

## Creating a ClusterIP Service

```
kubectl get pods -w

kubectl create deployment httpenv --image=bretfisher/httpenv

kubectl scale deployment/httpenv --replicas=5

kubectl expose deployment/httpenv --port 8888

kubectl get service

kubectl run --generator run-pod/v1 tmp-shell --rm -it --image bretfisher/netshoot -- bash

curl httpenv:8888

curl [ip of service]:8888

kubectl get service
```

<br/>

## Creating a NodePort and LoadBalancer Service

```

kubectl get all

kubectl expose deployment/httpenv --port 8888 --name httpenv-np --type NodePort

kubectl get services

curl localhost:32334

kubectl expose deployment/httpenv --port 8888 --name httpenv-lb --type LoadBalancer

kubectl get services

curl localhost:8888

kubectl delete service/httpenv service/httpenv-np

kubectl delete service/httpenv-lb deployment/httpenv
```

<br/>

## Kubernetes Services DNS

```
curl <hostname>

kubectl get namespaces

curl <hostname>.<namespace>.svc.cluster.local
```

<br/>

# Kubernetes Management Techniques

<br/>

## Run, Expose and Create Generators

```
kubectl create deployment sample --image nginx --dry-run -o yaml

kubectl create deployment test --image nginx --dry-run

kubectl create deployment test --image nginx --dry-run -o yaml

kubectl create job test --image nginx -dry-run -o yaml

kubectl expose deployment/test --port 80 --dry-run -o -yaml

kubectl create deployment test --image nginx

kubectl expose deployment/test --port 80 --dry-run -o -yaml

kubectl delete deployment test
```

<br/>

## The Future of Kubectl Run

```
kubectl run test --image nginx --dry-run

kubectl run test --image nginx --port 80 --expose --dry-run

kubectl run test --image nginx --restart OnFailure --dry-run

kubectl run test --image nginx --restart Never --dry-run

kubectl run test --image nginx --scheduled "_/1 _ \* \* \*" --dry-run
```

<br/>

## Imperative vs. Declarative

```
kubectl apply -f my-resources.yaml

kubectl run
```
