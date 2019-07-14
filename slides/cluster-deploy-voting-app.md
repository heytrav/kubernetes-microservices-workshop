### Deploying to Kubernetes Cluster



#### Setting up the Voting Application
* Have a look at kubernetes specs for the vote app
   ```
   cd ~/example-voting-app
   ```
   ```
   ls k8s-specifications
   ```
* Folder contains specification files for 
   + Deployments
   + Services


#### Creating a namespace
* <!-- .element: class="fragment" data-fragment-index="0" -->In dashboard click *Projects/Namespaces*
* <!-- .element: class="fragment" data-fragment-index="1" -->In the *Project Default* section, click *Add Namespace*
* <!-- .element: class="fragment" data-fragment-index="2" -->On next page
  enter **vote** in *Name* field and click *Create*
* <!-- .element: class="fragment" data-fragment-index="3" -->This creates a new namespace in you cluster
* <!-- .element: class="fragment" data-fragment-index="4" -->Can confirm by running in the shell
   ```
   kubectl get ns
   ```


#### Watch cluster
* <!-- .element: class="fragment" data-fragment-index="0" -->A couple ways to watch what is happening
* <!-- .element: class="fragment" data-fragment-index="1" -->In your terminal
   ```
   watch kubectl -n vote get all
   ```
* <!-- .element: class="fragment" data-fragment-index="2" -->In the dashboard
  - In *Project/Namespaces* menu
  - click on *Project: Default*
  - click on *Workloads* tab


#### Load Specification Files
<code>kubectl </code><code style="color:blue;">apply</code><code style="color:green;"> -f specfile.yml</code>

* The <!-- .element: class="fragment" data-fragment-index="0" -->`apply` command _applies_ a configuration to a specific resource
*  <!-- .element: class="fragment" data-fragment-index="1" -->The entire vote app is specified in yaml files
   ```
   cd ~/example-voting-app
   kubectl apply -n vote -f k8s-specifications
   ```
* <!-- .element: class="fragment" data-fragment-index="2" -->This tells Kubernetes to begin setting up containers
   + creates network endpoints
   + assigns Pods to replication controller
* When you run this, go back to the <!-- .element: class="fragment" data-fragment-index="3" -->_watcher_ terminal



#### Viewing Vote Website
* <!-- .element: class="fragment" data-fragment-index="0" -->Once all containers are running you can visit the *vote* and *result* apps
* <!-- .element: class="fragment" data-fragment-index="1" -->We need to know how to reach them
* <!-- .element: class="fragment" data-fragment-index="2" -->Both deployments are exposed with *NodePort* services
* <!-- .element: class="fragment" data-fragment-index="3" -->Can reach them if we know the IP of any node and the port the service is exposed on



#### Node IPs
* <!-- .element: class="fragment stretch" data-fragment-index="0" -->Use kubectl with <code>-o wide</code> to get node ips
   ```
   kubectl get nodes -o wide
   ```
   ```
    NAME            ....      EXTERNAL-IP      
    trainpc-01-*    ....      202.49.243.126   
    trainpc-01-*    ....      202.49.243.127   
    trainpc-01-*    ....      202.49.243.128   
   ```
* <!-- .element: class="fragment" data-fragment-index="1" -->Get services
   <pre><code data-trim data-noescape>
   kubectl -n vote get svc
	vote Services
	NAME      TYPE        CLUSTER-IP       ...   PORT(S)          AGE
	db        ClusterIP   10.108.228.228   ...   5432/TCP         3h
	redis     ClusterIP   10.107.101.100   ...   6379/TCP         3h
	result    NodePort    10.107.43.36     ...   5001:<mark>31001/TCP</mark>   3h
	vote      NodePort    10.104.244.69    ...   5000:<mark>31000/TCP</mark>   3h
</code></pre> <!-- .element: style="font-size:13pt;" -->
* <!-- .element: class="fragment" data-fragment-index="2" -->Use any of the
  node ips with port to view website



#### Exercise: Scale number of replicas for vote

* Increase the number of replicas (pods) for the _vote_ service
* <!-- .element: class="fragment" data-fragment-index="0" -->In the terminal
   <pre class="fragment" data-fragment-index="1"><code data-trim data-noescape>
      kubectl -n vote <mark>scale deployment vote</mark> --replicas=9
    </code></pre>
* <!-- .element: class="fragment" data-fragment-index="2" -->.. or try using dashboard UI
* Keep an eye on <!-- .element: class="fragment" data-fragment-index="3" -->_watcher_ terminal 
* Try varying number of replicas up and down<!-- .element: class="fragment" data-fragment-index="4" -->



##### Exercise:  Update voting app
* Update the _vote_ application with your image
   <pre><code data-trim data-noescape>
   kubectl -n vote <mark>set image</mark> deployment/vote \
            vote=YOURNAME/vote:v2
  </code></pre>
* Watch the _watcher_ terminal
* Refresh the site several times while update is running


#### Summary
* In this section we deployed a microservice application
* kubectl can scale services up or down
* Deployment rolling updates ensure that the application updates seemlessly
  with zero downtime
