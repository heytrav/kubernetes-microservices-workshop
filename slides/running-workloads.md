### Running Workloads in Kubernetes


#### Running Containerised Workloads
<code style="font-size:16pt;">kubectl run </code><code style="color:red;font-size:16pt;">name </code><code style="color:red;font-size:16pt;">--image=IMAGE:TAG</code><code style="color:green;font-size:16pt;"> OPTIONS</code>
* Create and run jobs in Kubernetes
* Example<!-- .element: class="fragment" data-fragment-index="0" -->:
   ```
   $ kubectl run nginx --image=nginx 
   ```
* Use get command to find out about container <!-- .element: class="fragment" data-fragment-index="1" -->
   ```
   $ kubectl get containers
   ```
   ```
   error: the server doesn't have a resource type "container"
   ```
   <!-- .element: class="fragment" data-fragment-index="2" -->
* Container isn't actually a resource type in Kubernetes <!-- .element: class="fragment" data-fragment-index="3" -->


#### Pods
* Technically you do not run  <!-- .element: class="fragment" data-fragment-index="0" -->_containers_ in Kubernetes
* The atomic <!-- .element: class="fragment" data-fragment-index="1" -->_run unit_ of Kubernetes is called a *_Pod_* 
* A Pod is an abstraction representing group <!-- .element: class="fragment" data-fragment-index="2" -->of ≥ 1 containers
   - images![pod and services](img/k8s-pods.png "Pods") <!-- .element: class="img-right" style="width:50%;" -->
   - network ports
   - volumes
* In this lesson we'll be using single container pods <!-- .element: class="fragment" data-fragment-index="3" -->


#### Pods
* Containers in a Pod share common resources   
   - Network IP address ![pod-anatomy](img/k8s-pod-anatomy.png "Pod upclose") <!-- .element: class="img-right" -->
   - Mounted volumes
   - Always co-located and co-scheduled
* Containers within a Pod communicate via _localhost_
Note: For this lesson we'll be using 1 container pods so the distinction isn't
that important. It is still good to be aware of the terminology


##### Exercise: Gather info about pods
* Use `kubectl get` to find info about running pods
   ```
   $ kubectl get pods
   ```
   ```
   NAME                     READY     STATUS    RESTARTS   AGE
   nginx-65899c769f-ttt2x   1/1       Running   0          1h
   ```
   <!-- .element: class="fragment" data-fragment-index="0" style="font-size:13pt;" -->


#### Running a Pod
* Let's run a <!-- .element: class="fragment" data-fragment-index="1" -->_ping_ command against Cloudflare's public DNS resolver
   ```
   kubectl run pingpong --image alpine ping 1.1.1.1
   ```
   ```
   deployment.apps "pingpong" created
   ```
* So, what is happening? <!-- .element: class="fragment" data-fragment-index="3" -->


#### View logs for a pod
* The `logs` command behaves the same as with `docker logs`
* Accepts either
   + pod name
      ```
      kubectl logs pingpong-abcde1234
      ```
   + type/name
   ```
   kubectl logs deploy/pingpong
   ```

|Option  | Description |
|--- | --- |
| -f, --follow | stream logs similar to `tail -f` |
| --tail <integer> | Specify how many lines from end to start with |
| --since | Get logs after a timestamp |


#### Watching pods
* The `-w` option to kubectl is like the `watch` command
   ```
   kubectl get pods -w
   ```
* In another window run the following:
   ```
   kubectl delete deploy/pingpong
   ```


#### Scheduling Pods

<code style="font-size:15pt;">kubectl run </code><code style="font-size:15pt;color:blue;">--schedule="\*/5 \* \* \* \* " ...</code>

* The <!-- .element: class="fragment" data-fragment-index="0" -->`--schedule=` option takes a cron-like time pattern
* Creates a type of pod that runs periodically at assigned times <!-- .element: class="fragment" data-fragment-index="1" -->
* In other words, a cronjob <!-- .element: class="fragment" data-fragment-index="2" -->

```
kubectl run pi --schedule="0/5 * * * ?" --image=perl \
   --restart=OnFailure --  \
       perl -Mbignum=bpi -wle 'print bpi(2000)'  
```
<!-- .element: class="fragment" data-fragment-index="3" -->

This pod calculates the value of PI to 2000 places every 5 minutes <!-- .element: class="fragment" data-fragment-index="4" -->
