### Kubernetes Networking


#### Kubernetes Networking Model
* A kubernetes cluster is essentially a big flat IP network
* Nodes and pods must be able to reach each other without a NAT
* Kubernetes doesn't mandate a specific implementation
* As result, there are dozens of implementations 
   + [some available implementations](https://kubernetes.io/docs/concepts/cluster-administration/networking/#how-to-implement-the-kubernetes-networking-model)


#### Simple Kubernetes Networking ![Scary Network](img/k8s-arch1.png "Scary Network Architecture")<!-- .slide: class="image-slide"  .element: width="50%" -->


#### Less Scary Networking ![networking light](img/k8s-arch2.png "Less Scary Network Architecture")


#### The Container Network Interface
* The CNI defines [specifications](https://github.com/containernetworking/cni/blob/master/SPEC.md#network-configuration) for network plugins
* Kubernetes delegates the network setup to CNI plugins
* CNI plugin
  + allocates an IP address
  + adds a network interface to pod's network namespace
  + configures the interface as required

