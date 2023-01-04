# Exposing Containers

    • kubectl expose creates a service for existing pods
    • A service is a stable address for pod(s)
    • If we want to connect to pod(s), we need a service
    • CoreDNS allows us to resolve services by name
    • There are different types of services
    • ClusterIP
    • NodePort
    • LoadBalancer
    • ExternalName

Now that you have your pods running, you're probably going to need to expose those to external services at some point. That means allowing them to accept connections, in some fashion, in your cluster or from outside your cluster.

In Kubernetes, we use the `kubectl expose` command as one of the ways to create a service.
A `service` is an endpoint that is consistent so that other things inside, or outside the cluster, might be able to access it.

When you create pods in Kubernetes, they don't automatically get a DNS name for external connectivity with an IP address, tight.

You would want to do that with creating a service on top of that existing pod. There's various ways besides this expose command to create a service.

# Basic Service Types

    • ClusterIP (default)
        - Single, internal virtual IP allocated
        - Only reachable from within cluster (nodes and pods)
        - Pods can reach service on apps port number
    • NodePort
        - High port allocated on each node
        - Port is open on every node’s IP
        - Anyone can connect (if they can reach node)
        - Other pods need to be updated to this port
        - These services are always available in Kubernetes
    •LoadBalancer
        - Controls a LB endpoint external to the cluster
        - Only available when infra provider gives you a LB (AWS ELB, etc)
        - Creates NodePort+ClusterIP services, tells LB to send to NodePort
    • ExternalName
        - Adds CNAME DNS record to CoreDNS only
        - Not used for Pods, but for giving pods a DNS name to use for something outside  Kubernetes
        - Kubernetes Ingress

The default service type is `ClusterIP`. It's only available in the cluster. This is really about one Kubernetes set of pods talking to another set of pods. That's going to be the DNS address in the core DNS control plane. It's going to get an IP address in that virtual IP address space inside the cluster. That allows your other pods running in the cluster to talk to this service using the port of the service. If you're running an Nginx app, and it was running on port 80 when you created the service, that service IP could also be on port 80. That keeps some sort of consistency there.

The next up here is `NodePort`, which is subtly different. The ClusterIP is the default and it always works inside the cluster. It doesn't need any firewall rules outside of the cluster for traffic to get to it.

But A NodePort is designed for something outside the cluster to talk to your service through the IP addresses on the nodes themselves. When you create a NodePort, you're going to get a high port on each node that's assigned to this service. Once you get that, you can update other things that need to know about this port. \

Next up is the `load balancer` type. This is mostly used in the cloud. The idea here is that you're controlling an external load balancer through the Kubernetes command line. Essentially, this is a bunch of automation. What you're doing here is in the background, when you create this load balancer, it's going to automatically create the ClusterIP in NodePort so that those are available. Then it's going to talk to the external system (e.g. AWS load balancer or some other cloud vendor).

The last of the four service types is `ExternalName`. This is used less often, and it doesn't really have anything to do with controlling inbound traffic to your services. This is more about stuff in your cluster needing to talk to outside services. You want to create DNS names in the core DNS system so that your cluster can resolve ExternalNames that you maybe don't have controlled externally. One of the reasons you might use ExternalName is when you're doing migrations of things.

<br/>

## Reference

[k8s/service](https://kubernetes.io/docs/concepts/services-networking/service/)
