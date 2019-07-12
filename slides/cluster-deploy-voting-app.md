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


#### Creating resources
<code>kubectl </code><code style="color:blue;">create </code><code style="color:green;">RESOURCE</code>
* Can create pods, services, etc. <!-- .element: class="fragment" data-fragment-index="0" -->
* Let's create a namespace for our application <!-- .element: class="fragment" data-fragment-index="1" -->

```
kubectl create namespace vote
```
<!-- .element: class="fragment" data-fragment-index="2" -->
```
namespace "vote" created
```
<!-- .element: class="fragment" data-fragment-index="3" -->


#### Watch cluster
* In another terminal, run the following

```
watch kubectl -n vote get all
```



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



#### Viewing Website
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
   <pre class="fragment" data-fragment-index="0"><code data-trim data-noescape>
      kubectl -n vote <mark>scale deployment vote</mark> --replicas=9
    </code></pre>
* Keep an eye on <!-- .element: class="fragment" data-fragment-index="1" -->_watcher_ terminal 
* Try varying number of replicas up and down<!-- .element: class="fragment" data-fragment-index="2" -->



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



### LoadBalancer Service
* <!-- .element: class="fragment" data-fragment-index="0" -->Using a NodePort service is ok for test purposes
* <!-- .element: class="fragment" data-fragment-index="1" -->Not practical for an actual website:
  - eg. visit my website at [http://202.49.243.126:31000](http://202.49.243.126:31000)
* <!-- .element: class="fragment" data-fragment-index="2" -->Prefer to use fixed domain and standard ports (i.e. 80, 443)


#### LoadBalancer Service
* <!-- .element: class="fragment" data-fragment-index="0" -->Let's create a load balancer service for the *vote* app
<pre><code data-noescape data-trim>
kind: Service
apiVersion: v1
metadata:
  name: loadbalanced-service
spec:
  selector:
    <mark>app: vote</mark>
  type: LoadBalancer
  ports:
  - name: http
    port: 80
    protocol: TCP
</code></pre>
* <!-- .element: class="fragment" data-fragment-index="1" -->Save this as `loadbalancer.yml`
* <!-- .element: class="fragment" data-fragment-index="2" -->Apply with kubectl
   ```
   kubectl -n vote apply -f loadbalancer.yml
   ```


#### Using a LoadBalancer service
* <!-- .element: class="fragment" data-fragment-index="0" -->Check available services to see when load balancer is ready
   ```
   kubectl -n vote get svc
   ```
* <!-- .element: class="fragment" data-fragment-index="1" -->It takes a few minutes for the load balancer to become active
* <!-- .element: class="fragment" data-fragment-index="2" -->Once finished a public IP will appear under EXTERNAL-IP
<pre style="font-size:11pt;"><code data-noescape data-trim>
kubectl -n vote get svc
NAME                   TYPE           CLUSTER-IP       EXTERNAL-IP      PORT(S)
db                     ClusterIP      10.254.70.29     &lt;none&gt;           5432/TCP
loadbalanced-service   LoadBalancer   10.254.167.242   <mark>202.49.243.158</mark>   80:31909/TCP
redis                  ClusterIP      10.254.125.187   &lt;none&gt;           6379/TCP
result                 NodePort       10.254.236.164   &lt;none&gt;           5001:31001/TCP
vote                   NodePort       10.254.234.53    &lt;none&gt;           5000:31000/TCP
</code></pre>


#### Advantages of LoadBalancer
* With a **LoadBalancer** type service you can now access your website on the
  new IP on a standard port (eg. 80 or 443)
* Can setup DNS with your domain name of choice
  - eg. Visit my website [http://my-vote-app.nz](http://www.latlmes.com/arts/return-of-the-golden-age-of-comics-1)


#### Disadvantages of a LoadBalancer
* Only work for one service
   - Have a LoadBalancer for *vote*
   - Need a separate LoadBalancer for *result* 
* LoadBalancer service is expensive

