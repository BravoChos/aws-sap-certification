## Kubernetes Services DNS

• Starting with 1.11, internal DNS is provided by CoreDNS
• Like Swarm, this is DNS-Based Service Discovery
• So far we've been using hostnames to access Services

```
curl <hostname>
```

• But that only works for Services in the same Namespace

```
kubectl get namespaces
```

Think of namesspaces as a way to section off all the different parts of different apps into these areas inside the same cluster, that won't really clash with each other. You can't technically create the same pod, or the same service, or the same Deployment, with the same names, in the same namespace.

• Services also have a FQDN

```
curl <hostname>.<namespace>.svc.cluster.local
```

## Reference

[k8s DNS specification](https://github.com/kubernetes/dns/blob/master/docs/specification.md)

[coreDND for k8s](https://www.coredns.io/plugins/kubernetes/)
