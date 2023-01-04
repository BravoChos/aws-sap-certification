# Install Kubernetes Locally

    • Kubernetes is a series of containers, CLI's, and configurations
    • Many ways to install, lets focus on easiest for learning
    • Docker Desktop: Enable in settings
    • Sets up everything inside Docker's existing Linux VM
    • Docker Toolbox on Windows: MiniKube
    • Uses VirtualBox to make Linux VM
    • Your Own Linux Host or VM: MicroK8s
    • Installs Kubernetes right on the OS

## Kubernetes In A Browser

Try http://play-with-k8s.com or katacoda.com in browser

    • Easy to get started
    • Doesn't keep your environment

## Docker Desktop (Recommended)

    • Runs/configures Kubernetes Master containers
    • Manages kubectl install and certs
    • Easily install, disable, and remove from Docker GUI

## MiniKube (for windows or linux)

• Download Windows Installer from GitHub
• minikube-installer.exe
• minikube start
• Much like the docker-machine experience
• Creates a VirtualBox VM with Kubernetes master setup
• Doesn't install kubectl

## MicroK8s (for linux)

• Installs Kubernetes (without Docker Engine) on localhost (Linux)
• Uses snap (rather then apt or yum) for install
• Control the MicroK8s service via microk8s. commands
• kubectl accessable via microk8s.kubectl
• Add CoreDNS for services to work
• microk8s.enable dns
• Add an alias to your shell (.bash_profile)
• alias kubectl=microk8s.kubectl
