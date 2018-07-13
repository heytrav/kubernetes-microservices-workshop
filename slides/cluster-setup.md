### Kubernetes Cluster


#### Setup a Kubernetes cluster
* Steps needed:
   + Create host machines in the cloud
   + Set up networking
   + Install Kubernetes dependencies
      - kubectl
      - kubeadm
      - kubelet
   + Join nodes to master


![fortune cookie](img/fortune-cookie.jpg "Fortune cookie")<!-- .slide: class="image-slide" -->


#### Bootstrapping a Cluster
* Setting up a Kubernetes cluster by hand is complicated
* Tools available to make this easier
   + Magnum
   + Google Kubernetes Environment
* Create an Ansible inventory file for your cluster


#### Create ansible config
* in `~/.ansible.cfg`
   ```
   [defaults]
   inventory = /home/USER/.ansible/inventory
   vault_password_file = /home/USER/.ansible/vault_password
   ```
* Replace USER with the user on your machine


#### Run local setup
```
cd ~/k8s-ansible
source venv/bin/activate
(venv) ansible-galaxy install -f -r requirements.yml
(venv) ansible-playbook local-setup.yml -e prefix=<username>
```


#### Create Kubernetes Cluster

```bash
ansible-playbook -K create-cluster-hosts.yml kubeadm-install.yml 
   -e prefix=<username> -e cloud_name=docker-training
```
<!-- .element: style="font-size:13pt;"  -->
* This playbook should do the following
  + Set up a cluster in OpenStack
  + Install Docker and Kubernetes libraries on servers
  + Initialise the _master_ node with `kubeadm`
  + Join worker nodes to cluster


#### Controlling Kubernetes Remotely
* Start kubectl proxy locally <!-- .element: class="fragment" data-fragment-index="0" -->
   ```bash
   kubectl --kubeconfig ~/k8s-admin.conf proxy
   Starting to serve on 127.0.0.1:8001
   ```
* Put this terminal aside and open a new one <!-- .element: class="fragment" data-fragment-index="1" -->
* All <!-- .element: class="fragment" data-fragment-index="2" -->`kubectl` calls must override server location
   ```
   kubectl --server=127.0.0.1:8001 ...
   ```



##### Exercise: Verify Kubernetes Cluster

* Verify nodes
    ```bash
    kubectl --server=127.0.0.1:8001 get nodes
    NAME               STATUS    ROLES     AGE       VERSION
    trainingpc-master   Ready     master    26m       v1.10.2
    trainingpc-worker1  Ready     <none>    25m       v1.10.2
    trainingpc-worker2  Ready     <none>    25m       v1.10.2
    ```
    <!-- .element: class="fragment" data-fragment-index="0" style="font-size:11pt;"-->


##### Exercise: Get JSON list of nodes with IPs
```
kubectl --server=127.0.0.1:8001 get nodes -o json | jq '.items[] | 
   {name: .metadata.name, ip: (.status.addresses[] 
            | select(.type == "InternalIP")) | .address }'
```
<!-- .element: class="fragment" data-fragment-index="0" style="font-size:13pt;" -->



#### Summary
* We've each (hopefully) have a functioning Kubernetes cluster
* Set up the control plane
* In the next section we'll deploy code to it
