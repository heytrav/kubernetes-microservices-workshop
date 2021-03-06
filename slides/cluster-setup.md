### Deploy a Kubernetes Cluster


#### Setup a Kubernetes cluster
* Cloud providers
   * [GKE](https://cloud.google.com/kubernetes-engine/)
   * [AWS EKS](https://aws.amazon.com/eks)
   * [Catalyst Cloud](https://dashboard.cloud.catalyst.net.nz/project/clusters)


#### OpenStack Command Line 
* OpenStack provides a command line interface
* `openstack` command line script written in Python
* Installed on your machines in a virtual environment
   - should see `venv` in your command prompt
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


#### Building your cluster
* Run the helper script
  ```
  ./create-cluster.sh

  ```



#### Accessing your cluster
* Creating a cluster is easy, but it takes a while (~10 to 15 min)
* One has been created for you already
* Query information about your cluster
   ```
   openstack coe cluster show  -f json $PREFIX | jq '{"name": .name, "status": .health_status}'
   ```
   <!-- .element: style="font-size:9pt;"  -->
* <!-- .element: class="fragment" data-fragment-index="0" -->Response
   ```
    {
    "name": "trainpc-01",
    "status": "HEALTHY"
    }
   ```

Note:
To set up the cluster run the following: 
```
create-cluster
```
Wait for the cluster to build by checking 
```
openstack coe cluster show -f json $PREFIX
```
Once the cluster is running, fetch the kube config file
```
setup-kubeconfig
```


#### Set up kubernetes config
* Retrieve the kubernetes config file from openstack
  ```
  ./setup-kubeconfig
  ```
* Creates the kubernetes config file
  ```
  ls ~/k8s-config
  ```
* We'll need to edit this later


#### Set up helper servers
* Kubernetes clusters are private by default
* Need to set up a *bastion* host to interact
* Change to the kubernetes infra repo
   ```
   cd ~/kubernetes-workshop-infra
   ansible-playbook create-infra-helpers.yml
   ```
* Follow instructions output by playbooks
* See [quickstart instructions](https://docs.catalystcloud.nz/kubernetes/quickstart.html#accessing-a-private-cluster)


#### Interacting with your cluster
* <!-- .element: class="fragment" data-fragment-index="0" -->As with minikube, you'll use `kubectl`
* <!-- .element: class="fragment" data-fragment-index="1" -->First we must configure `kubectl` to talk to our new cluster
* <!-- .element: class="fragment" data-fragment-index="2" -->`kubectl` can easily switch between different clusters or *contexts*
   ```
   kubectl config use-context minikube
   kubectl get nodes
   ```
* <!-- .element: class="fragment" data-fragment-index="3" -->Point it at the new cluster 
   ```
   kubectl config use-context default
   ```


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
kubectl get nodes -o json | jq '.items[] |  {name: .metadata.name, ip: (.status.addresses[] | select(.type == "ExternalIP")) | .address }' 
```
<!-- .element: class="fragment" data-fragment-index="0" style="font-size:9pt;" -->



#### Summary
* We each have a functioning Kubernetes cluster
* Can use `kubectl` to maintain multiple clusters
* Set up the control plane
