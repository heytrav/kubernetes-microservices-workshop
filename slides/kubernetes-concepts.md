### Kubernetes Resources


#### Kubernetes Resource Types
* Nodes
* Pod
* Deployment
* Namespaces
* Services
* Labels and Selectors


#### Nodes
* Nodes are where your containerised workloads will run![Orchestration](img/container-orchestration.svg "Container Orchestration")<!-- .element: class="img-right" width="50%" -->
* No upper limit on number of nodes in a Kubernetes cluster <!-- .element: class="fragment" data-fragment-index="0" -->
* Let's have a look at our <!-- .element: class="fragment" data-fragment-index="1" -->_minikube_ instance



#### Displaying Resources
<code>kubectl get </code><code style="color:red;">RESOURCE</code>
* Retrieve information about kubernetes resources <!-- .element: class="fragment" data-fragment-index="0" -->
    + eg. nodes


##### Exercise: Using `kubectl get`
* Use `kubectl get` to get info about current nodes
   ```
   $ kubectl get nodes
   ```
   <!-- .element: class="fragment" data-fragment-index="0" -->
   ```
   NAME       STATUS    ROLES     AGE       VERSION
   minikube   Ready     master    6d        v1.10.0
   ```
   <!-- .element: class="fragment" data-fragment-index="1" -->
* We currently only have one node named <!-- .element: class="fragment" data-fragment-index="1" -->_minikube_
* The default stdout is minimal <!-- .element: class="fragment" data-fragment-index="2" -->


#### Formatting output
* Many `kubectl` commands can output different data formats
  + yaml
  + json
* Pass `-o FORMAT` to command

```
Usage:
  kubectl get [(-o|--output=)json|yaml|wide|custom-columns=...|
   custom-columns-file=...|go-template=...|
   go-template-file=...|jsonpath=...|jsonpath-file=...]
```
<!-- .element: class="fragment" data-fragment-index="0" -->


##### Exercise: Get formatted data about nodes
* Output node information in JSON
   ```
   $ kubectl get nodes -o json
   ```
   ```json
   {
    "apiVersion": "v1",
    "items": [
        {
            "apiVersion": "v1",
            "kind": "Node",
            "metadata": {
                "annotations": {
                    "node.alpha.
                    "volumes.kub
   ```
   <!-- .element: class="fragment" data-fragment-index="0" -->
* Quite a bit more information to process <!-- .element: class="fragment" data-fragment-index="1" -->


##### Exercise: Process `kubectl` output
* It can be useful to pipe formatted output through other tools <!-- .element: class="fragment" data-fragment-index="0" -->
   + For example <!-- .element: class="fragment" data-fragment-index="1" -->[jq](https://stedolan.github.io/jq)
* Get a JSON list of node names with corresponding IP <!-- .element: class="fragment" data-fragment-index="2" -->
```
kubectl get nodes -o json | jq '.items[] |  {name: .metadata.name, ip: (.status.addresses[]  | select(.type == "InternalIP")) | .address }'
```
<!-- .element: class="fragment" data-fragment-index="3" style="font-size:10pt;" -->
```json
{
  "name": "minikube",
  "ip": "10.0.2.15"
}
```
<!-- .element: class="fragment" data-fragment-index="4" -->
