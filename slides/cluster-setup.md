### Kubernetes Cluster


#### Setup a Kubernetes cluster
* Alternative ways to create a cluster
  - Catalyst Cloud Open Stack Console
  - `openstack` command line client
* We'll use the client



#### OpenStack Command Line 
* OpenStack provides a command line interface
* `openstack` command line script written in Python
* Installed on your machines in a virtual environment
  ```
  /home/train/venv
  ```
* Everything should be setup


#### Interacting with Catalyst Cloud
* Try out the command line client
* Query existing templates
   ```
   openstack coe cluster template list
   ```
   <pre style="font-size:8pt;"><code data-notrim data-noescape>
   +--------------------------------------+----------------------------------+
   | uuid                                 | name                             |
   +--------------------------------------+----------------------------------+
   | 9c6e9df7-955a-465e-8460-e84e386624a0 | kubernetes-v1.11.6-prod-20190130 |
   | 4fcb04bd-22ba-4e1c-ab21-ff0339051d15 | kubernetes-v1.11.6-dev-20190130  |
   | b1d124db-b7cc-4085-8e56-859a0a7796e6 | kubernetes-v1.11.9-dev-20190402  |
   | cf337c0a-86e6-45de-9985-17914e78f181 | kubernetes-v1.11.9-prod-20190402 |
   | 967a2b86-8709-4c07-ae89-c0fe6d69d62d | kubernetes-v1.12.7-dev-20190403  |
   | f8fc0c67-84af-4bb8-89fb-d29f4c926975 | kubernetes-v1.12.7-prod-20190403 |
   +--------------------------------------+----------------------------------+
   </code></pre>


#### Creating a cluster
* Creating a cluster is easy, but it takes a while (~10 to 15 min)
* One has been created for you already
* Query information about your cluster
   ```
   openstack coe cluster show  -f json $PREFIX-k8s-test \
      | jq '{"name": .name, "status": .health_status}'
   ```
   ```
    {
    "name": "trainpc-01-k8s-test",
    "status": "HEALTHY"
    }
   ```


#### Interacting with your cluster
* As with minikube, you'll use `kubectl`
* Tell `kubectl` to talk to your new cluster
   ```
   kubectl config use-context cloud-k8s
   ```
* This tells `kubectl` to use the config for your cluster in Catalyst Cloud
  instead of the default one for minikube
* `kubectl` can easily switch between different clusters or *contexts*



##### Exercise: Verify Kubernetes Cluster

* Verify nodes
   ```bash
   kubectl get nodes
   ```
   ```
   NAME               STATUS    ROLES     AGE       VERSION
   trainpc-01-ivqn7i4nh66e-master-0   Ready    master   3h41m   v1.12.7
   trainpc-01-ivqn7i4nh66e-minion-0   Ready    <none>   3h41m   v1.12.7
   trainpc-01-ivqn7i4nh66e-minion-1   Ready    <none>   3h41m   v1.12.7
   ```
   <!-- .element: class="fragment" data-fragment-index="0" style="font-size:12pt;"-->

<!-- .element: class="stretch"  -->


##### Exercise: Get JSON list of nodes with IPs
```
kubectl get nodes -o json | jq '.items[] |  {name: .metadata.name, ip: (.status.addresses[] | select(.type == "InternalIP")) | .address }'
```
<!-- .element: class="fragment" data-fragment-index="0" style="font-size:10pt;" -->



#### Summary
* We each have a functioning Kubernetes cluster
* Can use `kubectl` to maintain multiple clusters
* Set up the control plane
