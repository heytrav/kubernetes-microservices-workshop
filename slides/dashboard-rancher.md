### Management Dashboard


#### Management Dashboards
* <!-- .element: class="fragment" data-fragment-index="0" -->Kubernetes has many moving parts
   - Services
   - Workloads
* <!-- .element: class="fragment" data-fragment-index="1" -->Lots of commands
  to remember for `kubectl`
* <!-- .element: class="fragment" data-fragment-index="2" -->Dashboards useful for managing as well as monitoring your cluster



#### Dashboard options
* Standard Kubernetes dashboard
   - As seen with `minikube dashboard`
   - Can setup using [instructions](https://docs.catalystcloud.nz/kubernetes/quickstart.html#accessing-the-kubernetes-dashboard) in Catalyst Cloud documentation
* Third party alternatives
  - RancherOS Kubernetes Dashboard


#### RancherOS dashboard
* Complete management interface
* Manage multiple clusters
* Lots of additional features
  - manage multiple authentication backends
  - launch applications
  - monitoring


#### Access the RancherOS dashboard
* <!-- .element: class="fragment" data-fragment-index="0" -->Open the management interface
 ```
 open-rancher
 ```
* <!-- .element: class="fragment" data-fragment-index="1" -->Click through the security warning
* <!-- .element: class="fragment" data-fragment-index="2" -->You'll need to set an admin password and confirm the page url
   - just use *admin* or something simple
* <!-- .element: class="fragment" data-fragment-index="3" -->Confirm the IP address
   - just click *Save URL*



#### Add Kubernetes Cluster
* Click on *Clusters* and _Add_ a cluster
* Click on **Import** button on the right under  *Import existing cluster* 
* Enter a name in the *Cluster Name* field
  - i.e. *sandbox*
* Click *create*


#### Add Kubernetes Cluster
* <!-- .element: class="fragment" data-fragment-index="0" -->Copy the command in the box with:
   ```
   curl --insecure -sfL ...
   ```
* <!-- .element: class="fragment" data-fragment-index="1" -->Paste and execute into your terminal
* <!-- .element: class="fragment" data-fragment-index="2" -->Click *Done* and select your new cluster from the list
* <!-- .element: class="fragment" data-fragment-index="3" -->In the following screen select your cluster 
* <!-- .element: class="fragment" data-fragment-index="4" -->It will take a few seconds/minutes to register with the dashboard


#### The RancherOS dashboard
* <!-- .element: class="fragment" data-fragment-index="0" -->Provides a main *Cluster* screen with some basic monitoring data (CPU,
  Memory, Pods)
* <!-- .element: class="fragment" data-fragment-index="1" -->We can also manage our cluster here; for example
   - setup authentication (OAuth, LDAP, etc.)
   - create namespaces
   - scale deployments
   - drain nodes
* <!-- .element: class="fragment" data-fragment-index="2" -->We will explore some of the features as we deploy our app in upcoming
  section


#### Add monitoring to our cluster
* <!-- .element: class="fragment" data-fragment-index="0" -->In the top menu, select _Tools_ and  _Monitoring_
* <!-- .element: class="fragment" data-fragment-index="1" -->Just scroll to bottom and click _Enable Monitoring_
* <!-- .element: class="fragment" data-fragment-index="2" -->Navigate back to your main cluster dashboard
* <!-- .element: class="fragment" data-fragment-index="3" -->Monitoring should be available in a couple minutes
* <!-- .element: class="fragment" data-fragment-index="4" -->Initially there won't be much to see so we'll check back later


#### Explore dashboard
* Namespaces
* Nodes
* Tools


#### Launch an app
* On far left tab drop down select *default*
* In the next menu select *Apps*
* Catalogue displays apps available has Helm charts
* Launch a Wordpress application




