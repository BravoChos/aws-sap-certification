# Basic Terms: System Parts

    • Kubernetes: The whole orchestration system
    • K8s <= "k-eights" or Kube for short
    • Kubectl: CLI to configure Kubernetes and manage apps
    • Using "cube control" official pronunciation
    • Node: Single server in the Kubernetes cluster
    • Kubelet: Kubernetes agent running on nodes
    • Control Plane: Set of containers that manage the
    cluster
        - Includes API server, scheduler, controller manager,etcd, and more
        - Sometimes called the "master"

**kubectl** is the command line tool that you will use to talk to the Kubernetes API. The main way we talk to Kubernetes is through its API. There's multiple tools out there that can do it. We'll be using most of the time is kubectl.

**Node**s are the servers that are inside of that cluster in Kubernetes.

**Kubelet** is the container that will run a small, little agent on each node to allow that node to talk back to the Kubernetes master. You can think as its own engine API that talks to the local Docker,or the local runtime.

The **control plane**, sometimes called the master,is what's in charge of the cluster. There could be one or more managers.

They take the Linux principle of do one thing and do it well, and they take that and split everything up. So, essentially each one of these parts is
So, essentially each one of these parts is doing one thing and doing it well, and it simplifies the design in terms of the development.

But when you have to build this and run it, it does make things a little harder to set up because there's more to it. This control plane includes containers that will be running the API, the scheduler, you actually need a database backend that will be something called etcd. Then you have controller manager. You'll probably need something called coreDNS to handle your DNS, and so on.

## Reference

[Kubernetis components](https://kubernetes.io/docs/concepts/overview/components/#master-components)
