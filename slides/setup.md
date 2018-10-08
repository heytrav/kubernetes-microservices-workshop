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
* Check out the Catalyst Cloud Ansible repo: <!-- .element: class="fragment" data-fragment-index="0" -->
   ```
   git clone https://github.com/catalyst/catalystcloud-ansible.git
   ```
   <!-- .element: style="font-size:12pt;" -->
* Run the install script <!-- .element: class="fragment" data-fragment-index="1" -->
   ```
   cd catalystcloud-ansible
   ./install-ansible.sh
   . 
   . <stuff happens>
   .
   source ansible-venv/bin/activate
   ```
   <!-- .element: style="font-size:12pt;"  -->
* We'll be using this virtualenv for tasks throughout the course <!-- .element: class="fragment" data-fragment-index="2" -->
* Might need to downgrade some libraries <!-- .element: class="fragment" data-fragment-index="3" -->
   ```
   pip install ansible==2.5.5 shade==1.28.0
   ```

<!-- .element: class="stretch"  -->


#### Course slides
* The course slides are available as nodejs presentation
   ```
   $ git clone https://github.com/heytrav/kubernetes-microservices-workshop
   $ cd ~/kubernetes-microservices-workshop/slides
   ```
   <!-- .element: style="font-size:12pt;"  -->
* To run them you'll need to have a recent nodejs
* Install nodejs and run the course slides
   ```
   npm install
   npm start
   ```
   <!-- .element: style="font-size:12pt;"  -->
* This should open a browser with the slides for this workshop


#### Checkout code for workshop
* Checkout more resources needed for course
   ```
   git clone https://github.com/heytrav/k8s-ansible.git
   ```
   <!-- .element: style="font-size:13pt;"  -->
* Run the `docker-install.yml` playbook
   ```
   $ cd k8s-ansible
   $ ansible-galaxy install -f -r requirements.yml
   $ ansible-playbook -i hosts docker-install.yml
   ```
* This should install:
   + Docker Community Edition
   + `docker-compose`
   + `minikube`
