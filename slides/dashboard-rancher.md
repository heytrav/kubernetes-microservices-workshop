### Management Dashboard


#### Dashboard options
* Standard Kubernetes dashboard
   - As seen with `minikube dashboard`
   - Follow the [setup instructions](https://docs.catalystcloud.nz/kubernetes/quickstart.html#accessing-the-kubernetes-dashboard)
* RancherOS Kubernetes Dashboard


#### RancherOS dashboard
* Complete management interface
* Manage multiple clusters
* Lots of additional features
  - manage multiple authentication backends
  - launch applications
  - monitoring


#### Access the RancherOS dashboard
* Navigate to the management interface
 ```
 open-rancher
 ```
* Should open up a tab in firefox
* You'll need to set an admin password and confirm the page url



#### Add authentication
##### Demo
* Click on the *Security* tab
* Let's set up an authentication backend using GitHub
* Note that you will need to be able to log in to GitHub
* Follow directions in interface to add a cluster


#### Add Kubernetes Cluster
* Click on *Clusters* and _Add_ a cluster
* Click on *Import existing cluster* on the right
* Select a name, can be anything you want
* Click *create*


#### Add Kubernetes Cluster
* Copy *curl* command at the bottom
* Paste and execute in your terminal
* Click *Done* and select your new cluster from the list
* It will take a few seconds/minutes to register with the dashboard


#### Add monitoring to our cluster
* In the top menu, select _Tools_ and  _Monitoring_
* Just scroll to bottom and click _Enable Monitoring_
* Navigate back to your main cluster dashboard
* Monitoring should be available in a couple minutes
* Initially there won't be much to see so we'll check back later


#### Explore dashboard
* Namespaces
* Nodes
* Tools


#### Launch an app
* On far left tab drop down select *default*
* In the next menu select *Apps*
* Catalogue displays apps available has Helm charts
* Launch a Wordpress application




