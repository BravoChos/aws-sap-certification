# Creating a ClusterIP Service

• Open two shell windows so we can watch this

```
kubectl get pods -w
```

This is like a watch command where it will keep running and show us over time as things change.

• In second window, lets start a simple http server using sample code

```
kubectl create deployment httpenv --image=bretfisher/httpenv
```

httpenv is a very simple HTTP Web server that essentially when you hit it with a cURL, it just spits back all the environment variables it's getting at the command line.

• Scale it to 5 replicas

```
kubectl scale deployment/httpenv --replicas=5
```

The scale command is useful with a Deployment because it allows us to change the number of replicas in a single,friendly command.

• Let's `create a ClusterIP service` (default)

```
kubectl expose deployment/httpenv --port 8888
```

This will tell it which Deployment to expose and the port that that Deployment is listening on.
Cluster IP is only usable inside the cluster for nodes and other pods to be able to access it.

## Inspecting ClusterIP Service

• Look up what IP was allocated

```
kubectl get service
```

• Remember this IP is cluster internal only, how do we curl it?

1. If you're on Docker Desktop (Host OS is not container OS)

```
kubectl run --generator=run-pod/v1 tmp-shell --rm -it --image bretfisher/netshoot -- bash
curl httpenv:8888
```

We're going to use the --rm here which means once the pod stops, go ahead and remove it. The -it gives us a shell into that pod once we hit the enter command. Then --image is telling us what image we prefer. In this case, we're using my netshoot image, which is a whole bunch of different networking and Linux utilities in it. One of which is cURL.

2. If you're on Linux host

```
curl [ip of service]:8888
```

If you're on Linux, there's an easier way. Because the way that Kubernetes works is that all nodes and containers, by default, can talk to each other out-of-the-box. The node that you're on, assuming that you're running Kubernetes on that local machine, has access to all of these private IP addresses.
