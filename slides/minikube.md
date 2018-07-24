### Kubernetes on your workstation


#### Minikube
* Creates a _single node_ kubernetes cluster on your PC
* Useful for blah
* Practice with kubernetes


#### Setting up Minikube

* Install a hypervisor
  + [KVM](https://www.linux-kvm.org/page/Main_Page)
  + [virtualbox](https://www.virtualbox.org/wiki/Downloads)
* [Install minikube](https://kubernetes.io/docs/tasks/tools/install-minikube/)



#### Start Minikube
* Start minikube
   ```
   minikube start
   ```
* This will configure `~/.kube/config` to speak to local cluster


#### Interacting with minikube
* Find  ip of cluster
   ```
   minikube ip
   ```
* Use `kubectl` to control a minikube cluster
Note: As with any kubernetes cluster



#### Minikube Dashboard
* To view the minikube dashboard
   ```
   minikube dashboard
   ```
