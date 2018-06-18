### Controlling Kubernetes


#### Controlling a Kubernetes Cluster


##### `kubectl`
* The client tool for interacting with Kubernetes REST API
* A very rich CLI tool
* Pronounced:
  + _cube C T L_
  + _cube C D L_
  + _cube cuddle_



#### Configuring `kubectl`
* Configuration file for `kubectl` 
   + `~/.kube/config`
   + using `--kubeconfig` to pass a configuration
* Override via specific CLI options; ie:
   + `--server`
   + `--user`
* `kubectl` currently configured to interact with minikube 


### `kubectl` and minikube



#### Inline documentation
* Use `-h` option to get an overview of commands 
   <pre style="font-size:10;"><code data-trim data-noescape>
   $ kubectl -h  
   kubectl controls the Kubernetes cluster manager. 
   
   Find more information at: https://kubernetes.io/docs/reference/kubectl/overview/
   
   Basic Commands (Beginner):
     create         Create a resource from a file or from stdin.
     expose         Take a replication controller, service, deployment or pod and
   <!-- .element: style="font-size:10;"  -->

</code></pre>   
* Note that they are sorted from _beginner_ to _advanced_

<!-- .element: class="stretch"  -->


#### Command documentation
* Use `kubectl COMMAND -h` to get usage for any commands


#### Explain resources
* Use `kubectl explain RESOURCE` to see info about specific kubernetes resources
  + pods
  + nodes
  + deployments
  + etc.

```
$ kubectl explain ns

KIND:     Namespace
VERSION:  v1

DESCRIPTION:
     Namespace provides a scope for Names. Use of multiple namespaces is
     optional.
```
<!-- .element: class="fragment" data-fragment-index="0" style="font-size:10;" -->



#### Gathering information
* Use `get` to retrieve information about kubernetes resource objects
  ```
  kubectl get RESOURCE
  ```
  + nodes
  + pods
  + deployments

* A number of objects can be abbreviated
   + `kubectl get nodes`
   + `kubectl get no`
   + `kubectl get services`
   + `kubectl get svc`


#### Formatting output
* `kubectl` output different formats
  + yaml
  + json
  + custom

```
Usage:
  kubectl get
[(-o|--output=)json|yaml|wide|custom-columns=...|custom-columns-file=...|go-template=...|go-template-file=...|jsonpath=...|jsonpath-file=...]
```
<!-- .element: class="fragment" data-fragment-index="0" -->


##### Exercise: Get list of nodes
* Output node information in YAML or JSON

```
kubectl get nodes -o yaml
```
<!-- .element: class="fragment" data-fragment-index="0" -->


##### Exercise: Get list of pods
* 
