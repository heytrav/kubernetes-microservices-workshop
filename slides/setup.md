### Setting up


#### Course Prerequisites
(things we won't be covering)
* Linux/Unix
   + working with a shell
   + navigating directories
* Basic understanding of Docker
   + commands and usage
   + How to run containers
* Account with [Docker Hub](https://hub.docker.com)


#### Training Environment
* Training machines
   + Ubuntu 18.04?
   + Ubuntu 14.04



#### Install some dependencies
* Ansible
* Docker
* `docker-compose`
* `minikube`

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

<!-- .element: class="stretch"  -->


#### Course slides
* The course slides are available as nodejs presentation
   ```
   $ git clone https://github.com/heytrav/scaleconf-2018-kubernetes.git
   $ cd ~/scaleconf-2018-kubernetes/slides
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
