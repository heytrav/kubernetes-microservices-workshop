# Docker Role

A role for installing Docker on a set of hosts.

## Description


To use, just include the role in a play:

```
- name: Install docker on gitlab machine
  hosts: machines
  become: yes
  roles: [docker]
  tasks:
  
    - name: Some tasks

```


Note: At the moment this only supports Ubuntu.
