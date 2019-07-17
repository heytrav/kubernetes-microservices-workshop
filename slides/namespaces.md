### Namespaces


#### Namespaces
* A way to partition a Kubernetes cluster for different applications
* Partition physical cluster into virtual clusters ![namespaces](img/k8s-namespaces.png "Namespaces") <!-- .element: class="img-right" -->


##### Exercise: Get list of namespaces
* Use `kubectl` to get list of namespaces
   ```
   $ kubectl get namespace
   ```
   ```bash
    NAME              STATUS   AGE
    default           Active   8m44s
    kube-node-lease   Active   8m47s
    kube-public       Active   8m47s
    kube-system       Active   8m47s
   ```
   <!-- .element: class="fragment" data-fragment-index="0" -->



#### Namespaces in Kubernetes
* Kubernetes has 3 namespaces out of the box
  + default
    - Unless otherwise specified, objects will be created or queried here
  + kube-public
    - Reserved for cluster usage for resources that should be visible
      throughout cluster
  + kube-node-lease
    - Added in 1.14; a new way to implement node heartbeats
  + kube-system
    - Reserved for Kubernetes control 


#### Operating in specific namespace
<code>kubectl <code style="color:blue;">-n namespace </code>COMMAND </code><code style="color:red;">RESOURCE</code>
* Specify a namespace with<!-- .element: class="fragment" data-fragment-index="2" -->*`-n <namespace>`* flag
   ```bash
   $ kubectl -n kube-system get pods
   ```
   ```
   NAME                                    READY     STATUS    RESTARTS   AGE
   etcd-minikube                           1/1       Running   0          1h
   kube-addon-manager-minikube             1/1       Running   3          2d
   kube-apiserver-minikube                 1/1       Running   0          1h
   kube-controller-manager-minikube        1/1       Running   0          1h
   kube-dns-86f4d74b45-nqx7c               3/3       Running   12         2d
   kube-proxy-z4qqs                        1/1       Running   0          1h
   kube-scheduler-minikube                 1/1       Running   3          2d
   kubernetes-dashboard-5498ccf677-ccvnq   1/1       Running   7          2d
   storage-provisioner                     1/1       Running   8          2d
   ```
   <!-- .element: class="fragment" data-fragment-index="3" -->


#### `kube-system` namespace
* `kube-system` is used for the control plane
* Pods in this namespace _are_ Kubernetes
  + `etcd` (eht-see-dee) simple storage for k8s
  + `kube-apiserver` The API server
  + `kube-controller-manager` and `kube-scheduler`
  + `kube-dns` Manages internal DNS
  + `kube-proxy` (on each machines) manages port mappings


#### Creating namespaces
<code>kubectl create </code><code style="color:red;">namespace NAME</code>
* The create command can be used to create a new namespace
* Let's create a namespace
   ```
   $ kubectl create namespace cats
   ```
* Verify that the new namespace exists <!-- .element: class="fragment" data-fragment-index="0" -->
   ```
   $ kubectl get ns
   ```
   ```
    NAME          STATUS    AGE
    cats          Active    2h
    default       Active    2h
    kube-public   Active    2h
    kube-system   Active    2h
   ```
   <!-- .element: class="fragment" data-fragment-index="1" -->


##### Create application in namespace
* Let's spin up an application in our new namespace
   ```
   kubectl run --generator=run-pod/v1 -n cats cat-app  --port=5000  \
       --image=heytrav/cat-of-the-day:v1
   ```
* Query state of pod/deployments in <!-- .element: class="fragment" data-fragment-index="0" -->_cats_ namespace
   ```
   kubectl -n cats get pods
   ```
   ```
   NAME                      READY     STATUS    RESTARTS   AGE
   cat-app-b848f798f-clrvd   1/1       Running   0          2h
   ```
   <!-- .element: class="fragment" data-fragment-index="1" style="font-size:13pt;" -->
