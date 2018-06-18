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



#### Bootstrapping a Cluster
* Setting up a Kubernetes cluster by hand is complicated
* Tools available to make this easier
   + Magnum
   + Google Kubernetes Environment
* Create an Ansible inventory file for your cluster
```
cd ~/k8s-ansible
source venv/bin/activate
(venv) ansible-playbook local-setup.yml -e prefix=<username>
```


### Create Kubernetes Cluster

```
ansible-playbook -K -i cloud-hosts \
   create-cluster-hosts.yml kubeadm-install.yml -e prefix=<username>
```



### Remotely Controlling Kubernetes
* Start kubectl proxy locally
   ```
   kubectl --kubeconfig ~/k8s-admin.conf proxy
   Starting to serve on 127.0.0.1:8001
   ```
* Put this terminal aside and open a new one



### Verify Kubernetes Cluster
```
kubectl --server=127.0.0.1:8001 get nodes
NAME               STATUS    ROLES     AGE       VERSION
trainingpc-master   Ready     master    26m       v1.10.2
trainingpc-worker1  Ready     <none>    25m       v1.10.2
trainingpc-worker2  Ready     <none>    25m       v1.10.2
```
