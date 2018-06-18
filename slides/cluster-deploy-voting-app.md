### Deploying to Kubernetes Cluster



### Setting up the Voting Application
* Have a look in the `example-voting-app/k8s-specifications`



### Create Namespace
* Create a namespace for our application

```
kubectl  --server=127.0.0.1:8001 create namespace vote
namespace "vote" created
```


### Watch cluster
* In another terminal, run the following

```
watch -t -n1 'echo Vote Pods \
   && kubectl --server=127.0.0.1:8001 get pods -n vote -o wide \
   && echo && echo vote Services \
   && kubectl --server=127.0.0.1:8001 get svc -n vote \
   && echo && echo vote Deployments \
   && kubectl --server=127.0.0.1:8001 get deployments -n vote \
   && echo && echo Nodes \
   && kubectl --server=127.0.0.1:8001 get nodes -o wide'
```



### Load Specification Files

* The `apply` command loads a specification into kubernetes
   ```
   kubectl apply <file> 
   ```
* The entire vote app is specified in yaml files
```bash
cd ~/example-voting-app/k8s-specifications
for i in `ls *.yaml`; \
     do kubectl --server=127.0.0.1:8001 apply -n vote -f $i; done
```
<!-- .element: style="font-size:12pt;"  -->

* This tells kubernetes to begin setting up containers
  + creates network endpoints
  + assigns Pods to replication controller
* When you run this, go back to the _watcher_ terminal



### View Website
* Once all containers are running you can visit your website
* You first need to find a couple ports:
   <pre><code data-trim data-noescape>
	vote Services
	NAME      TYPE        CLUSTER-IP       ...   PORT(S)          AGE
	db        ClusterIP   10.108.228.228   ...   5432/TCP         3h
	redis     ClusterIP   10.107.101.100   ...   6379/TCP         3h
	result    NodePort    10.107.43.36     ...   5001:<mark>31001/TCP</mark>   3h
	vote      NodePort    10.104.244.69    ...   5000:<mark>31000/TCP</mark>   3h
</code></pre> <!-- .element: style="font-size:13pt;" -->
* Navigate to the [voting app](http://voting:appl:31000). You may need to
  change the port


### Scaling 

* Orchestration platforms make it easy to scale your app up/down
   + Simply increase or decrease the number of containers
* Let's increase the number of vote containers
   ```
   kubectl --server=127.0.0.1:8001 -n vote scale deployment vote --replicas=9
   ```
   <!-- .element: style="font-size:13pt;" -->
* Play with the scaled number; keep an eye on _watcher_ terminal 



###  Updating Our Application
* Update the _vote_ application with your image
   ```
   kubectl --server=127.0.0.1:8001  \
        -n vote set image deployment/vote \
            vote=YOURNAME/vote:v1
   ```
* Watch the _watcher_ terminal
* Refresh the site several times while update is running



### Kubernetes Dashboard
* Kubernetes provides a dashboard for monitoring purposes
   ```
   kubectl --server=127.0.0.1:8001 -n kube-system apply -f \
       https://raw.githubusercontent.com/kubernetes/dashboard/master/src/deploy/recommended/kubernetes-dashboard.yaml
   ```
* Once you've activated it, go to the [dashboard page](http://127.0.0.1:8001/api/v1/namespaces/kube-system/services/https:kubernetes-dashboard:/proxy/)



### Clean up

```
ansible-playbook ansible/remove-cluster-hosts.yml -K -e prefix=<username>
```
