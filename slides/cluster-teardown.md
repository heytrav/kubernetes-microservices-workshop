## The End
Note: Clean up steps:
```
helm delete my-nginx
delete-cluster
ansible-playbook -i ~/.ansible/inventory/cloud-hosts \
   -i inventory/openstack remove-rancheros-cluster.yml \
   -K -e node=manager
```
