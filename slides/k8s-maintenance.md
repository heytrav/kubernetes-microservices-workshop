### Maintaining clusters


#### Updating Nodes
* Important to maintain up-to-date stack
* Security updates and patches for underlying OS
* This section explores regular maintenance task on a k8s cluster
* It's good to regularly update machines
* Easiest way is to simply replace VMs on a regular basis


#### Draining nodes
<code>kubectl </code><code style="color:blue;">drain</code><code style="color:green;"> OPTIONS</code>
* Tell kubernetes to take a node out of service
* Node is _cordoned_ off
* Pods will be respawned on other machines
* K8s will not restart any Pods until node is _uncordoned_


#### Drain Node <!-- .slide: class="image-slide" -->
![k8s-drain](img/k8s-drain-expand.png "Expand")



#### Adding back a node
<code>kubectl </code><code style="color:blue;">uncordon</code><code style="color:red;"> node</code>
* Uncordon returns or adds a cordoned node back to service
* K8s will not immediately add pods to node
   + culling/respawning
   + scale operations


#### Uncordon Node <!-- .slide: class="image-slide" -->
![drain-uncordon](img/k8s-drain-build-replacement.png "Drain")



#### Managing maintenance
* Dashboard provides some tooling for draining/uncordoning nodes
* Ideally your cloud provider will do this for you
  - Drain/Cordon
  - patching/replacing nodes
* cluster options
  - built in
  - trigger via API call



#### Summary
* Rebuilding nodes on a regular basis essential for security
* K8s provides means for coordinating stack maintenance
* Draining and rebuilding nodes easy to automate
