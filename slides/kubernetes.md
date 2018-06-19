## Kubernetes


### Kubernetes Facts

* Greek word for _helmsman_ or _pilot_
* Also origin of words like _cybernetics_ and _government_
* Inspired by _Borg_, Google's internal scheduling tool
* Play on _Borg cube_
* [Source](https://news.ycombinator.com/item?id=9653797)


### Kubernetes Concepts
* Host types
   + master
      - performs _scheduling_
      - monitoring/healthchecks
   + node (formerly _minion_)
      - runs containers


### Pods
* A _pod_ is the unit of work 
   + Consist of ≥ 1 containers ![pod and services](img/pod-diagram.svg "Pod and Services") <!-- .element: class="img-right" style="width:50%;" -->
      - Always _scheduled_ together
      - Have same IP
      - Communication via localhost


### Deployments

* Provides declarative updates for Pods
* Describe _desired state_ of an object and controller changes state at a
  controlled rate
* Functions
   + Create pods
   + Declare new state of pods
   + Scale deployment
   + Rollback to an earlier deployment revision



### Services
* Exposes IP of Pod to ![kubernetes interaction](img/kubernetes-user-interaction.svg "Kubernetes Architecture") <!-- .element: class="img-right" style="width:50%;" -->
    + Other Pods
    + External ports (i.e. web, API ingress)



### Labels & Selectors
* Label is a key: value pair used to group objects
    - replication controllers for scheduling pods
    - services 
* Label Selectors 
   + Select objects base on labels
   + Semantics:
      - `role = webserver` 
      - `app != foo`, 
      - `role in (webserver, backend)`


### Namespaces
* Virtual cluster
* Isolate set of containers on same physical cluster


### Kubernetes Labels & Deployments <!-- .slide: class="image-slide" -->
![label-selectors](img/label-selectors.svg "Label Selectors") 



### Defining a Service
* Service spec defines
  + Type <!-- .element: class="fragment" data-fragment-index="0" -->
     - <!-- .element: class="fragment" data-fragment-index="1" -->`NodePort | ClusterIP`
  + Ports & protocol <!-- .element: class="fragment" data-fragment-index="2" -->
  + Map to Replication Controller (Pod) <!-- .element: class="fragment" data-fragment-index="3" -->

<!-- .element: style="width:50%;float:left;"  -->

<pre style="width:40%;float:left;"><code data-trim data-noescape>
apiVersion: v1
kind: Service
metadata:
  name: redis
spec:
  <span class="fragment" data-fragment-index="1"><mark>type: ClusterIP</mark></span>
  <span class="fragment" data-fragment-index="2">ports:
  - port: 6379
    targetPort: 6379</span>
  <span class="fragment" data-fragment-index="3">selector:
    <mark>app: redis</mark></span></code></pre>



### Defining a Deployment
* Specification deployment file
* Attributes define <!-- .element: class="fragment" data-fragment-index="0" -->
   + How many instances to run at start<!-- .element: class="fragment" data-fragment-index="1" -->
   + Label selectors <!-- .element: class="fragment" data-fragment-index="1" -->
   + Images/containers in pod <!-- .element: class="fragment" data-fragment-index="2" -->
   + Volumes mounted in pod <!-- .element: class="fragment" data-fragment-index="3" -->

<!-- .element: style="width:50%;float:left;"  -->

<pre  style="width:40%;float:left;font-size:10pt;" ><code data-trim data-noescape>
<span class="fragment" data-fragment-index="0">apiVersion: extensions/v1beta1
kind: Deployment
metadata:
  name: redis</span>
<span class="fragment" data-fragment-index="1">spec:
  <span class="fragment" data-fragment-index="1"><mark>replicas: 1</mark></span>
  template:
    metadata:
      labels:
        <mark>app: redis</mark></span>
    <span class="fragment" data-fragment-index="2">spec:
      containers:
      - <mark>image: redis:alpine</mark>
        name: redis
        volumeMounts:
        - mountPath: /data
          name: redis-data</span>
      <span class="fragment" data-fragment-index="3">volumes:
      - name: redis-data
        emptyDir: {}</span> 
</code></pre>

