### Controlling Kubernetes


##### `kubectl`
* The client tool for interacting with Kubernetes REST API
* Tons of functionality
* Pronounced:
  + _cube C T L_
  + _cube C D L_
  + _cube cuddle_



#### Kubernetes Control Plane
* kubectl
   - client API interface for kubernetes control plane
* api server ![control-plane](img/k8s-master-control.png "Kubernetes Control Plane") <!-- .element: class="img-right"  width="60%"-->
   - REST frontend
+ controller manager
   - replication
   - deployment
+ etcd
   - key/value storage

<!-- .element: style="font-size:19pt;"  -->



#### Inline documentation
<code>kubectl </code><code style="color:red;">-h</code>
* Use `-h` option to get an overview of commands 
   <pre style="font-size:10;"><code data-trim data-noescape>
   $ kubectl -h  
   kubectl controls the Kubernetes cluster manager. 
   
   Find more information at: https://kubernetes.io/docs/reference/kubectl/overview/
   
   Basic Commands (Beginner):
     create         Create a resource from a file or from stdin.
     expose         Take a replication controller, service, deployment or pod and
</code></pre>   
* Note that they are sorted from _beginner_ to _advanced_
<!-- .element: class="stretch"  -->


#### Command documentation
<code>kubectl </code><code style="color:green;">COMMAND </code><code>-h</code>
* Get usage for any commands
<!-- .element: class="stretch"  -->

```
$ kubectl run -h
Create and run a particular image, possibly replicated. 

Creates a deployment or job to manage the created container(s).

Examples:
  # Start a single instance of nginx.
  kubectl run nginx --image=nginx
```
<!-- .element: class="fragment" data-fragment-index="0" style="font-size:12pt;" -->


#### Get documentation about resources in Kubernetes
<code>kubectl explain </code><code style="color:red;">RESOURCE</code>
* In Kubernetes we manage objects, or _resource types_ eg.
   + nodes
   + pods
   + namespaces
* The <!-- .element: class="fragment" data-fragment-index="0" -->`explain` command displays documentation about specific kubernetes resources 



#### Exercise: Ask `kubectl` about resources
* Use `kubectl explain` to find out about
   + nodes
   + namespaces
   + pods
   + services
* These are typical _resource types_ in Kubernetes

```
$ kubectl explain node
KIND:     Node
VERSION:  v1

DESCRIPTION:
     Node is a worker node in Kubernetes. Each node will have a unique
     identifier in the cache (i.e. in etcd).

FIELDS:
   apiVersion   <string>
     APIVersion defines the versioned schema of this representation of an
     object. Servers should convert recognized schemas to the latest internal
     value, and may reject unrecognized values. More info:
     https://git.k8s.io/community/contributors/devel/api-conventions.md#resources
```
<!-- .element: class="fragment" data-fragment-index="0" style="font-size:10pt;" -->



#### Configuring `kubectl`
* Minikube set up a configuration file for us
   + `~/.kube/config`
* Make sure we are using minikube's config
  ```
  kubectl config use-context minikube
  ```
* Configuration file for `kubectl` 
   + pass a configuration file with `--kubeconfig`
