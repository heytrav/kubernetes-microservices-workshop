### Setting up


#### Course Prerequisites
* Account with [Docker Hub](https://hub.docker.com)
   + take a few minutes to set one up
* Linux/Unix
   + working with a shell
   + navigating directories
* Basic understanding of Docker
   + commands and usage
   + How to run containers


#### Training Environment
* In this course we'll be using <!-- .element: class="fragment" data-fragment-index="0" -->
   + Docker Community Edition
   + `docker-compose`
   + Ansible
   + minikube
* Training machines should be setup <!-- .element: class="fragment" data-fragment-index="1" -->
   + Ubuntu (trusty or xenial)
* Following slides contain instructions for setting up environment <!-- .element: class="fragment" data-fragment-index="2" -->



#### Install some dependencies
* [Ansible](http://docs.ansible.com/ansible/latest/intro_installation.html)
* [Docker Community Edition](https://store.docker.com/search?offering=community&type=edition)
* [docker-compose](https://docs.docker.com/compose/install/)
* [minikube](https://kubernetes.io/docs/tasks/tools/install-minikube/)
  + [KVM](https://www.linux-kvm.org/page/Main_Page)
  + [virtualbox](https://www.virtualbox.org/wiki/Downloads)

Note: some of these should be done anyway but you might have to walk through
them anyway


### Setup Ansible
* Create and activate a python virtual environment <!-- .element: class="fragment" data-fragment-index="0" -->
   ```
   virtualenv -p /usr/bin/python3 ~/venv
   source ~/venv/bin/activate
   ```
* Install Ansible and some additional dependencies <!-- .element: class="fragment" data-fragment-index="1" -->
   ```
   pip install ansible openstacksdk shade
   ```
* We'll be using this virtualenv for tasks throughout the course <!-- .element: class="fragment" data-fragment-index="2" -->
* Might need to downgrade some libraries <!-- .element: class="fragment" data-fragment-index="3" -->
   ```
   pip install ansible==2.5.5 shade==1.28.0
   ```

<!-- .element: class="stretch"  -->


#### Course slides
* The course slides are available as nodejs presentation <!-- .element: class="fragment" data-fragment-index="0" -->
   ```
   git clone https://github.com/heytrav/kubernetes-microservices-workshop
   ```
   <!-- .element: style="font-size:12pt;"  -->
* Run playbook to install nodejs and setup reveal presentation <!-- .element: class="fragment" data-fragment-index="1" -->
   ```
   cd ~/kubernetes-microservices-workshop/setup
   ansible-galaxy install -f -r requirements.yml
   ansible-playbook -K -i hosts setup.yml
   ```
* Run the course slides <!-- .element: class="fragment" data-fragment-index="2" -->
   ```
   cd ~/kubernetes-microservices-workshop/slides
   npm start
   ```
   <!-- .element: style="font-size:12pt;"  -->
* This should open a browser with the slides for this workshop <!-- .element: class="fragment" data-fragment-index="3" -->


#### Setup machine for workshop
* Setup Ansible roles for project <!-- .element: class="fragment" data-fragment-index="0" -->
   ```
   cd ~/k8s-ansible
   ansible-galaxy install -f -r requirements.yml
   ```
* Run playbook to setup some configuration <!-- .element: class="fragment" data-fragment-index="1" -->
   ```
   ansible-playbook -i inventory/hosts k8s-workshop-setup.yml
   ```
* Run a second time to install dependencies <!-- .element: class="fragment" data-fragment-index="2" -->
   ```
   ansible-playbook -i inventory/training k8s-workshop-setup.yml -K
   ```
