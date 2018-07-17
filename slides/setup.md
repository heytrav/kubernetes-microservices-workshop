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
```
git clone https://github.com/catalyst/catalystcloud-ansible.git
```

<!-- .element: style="width:100%;" class="fragment" data-fragment-index="0" -->

```
cd ~/catalystcloud-ansible
./install-ansible.sh
. 
. <stuff happens>
.
source $CC_ANSIBLE_DIR/ansible-venv/bin/activate
```
<!-- .element: style="width:100%;" class="fragment" data-fragment-index="1" -->

* Installs python virtualenv with latest ansible libraries <!-- .element: class="fragment" data-fragment-index="2" -->
* We'll be using this virtualenv for tasks throughout the course <!-- .element: class="fragment" data-fragment-index="3" -->

<!-- .element: style="width:80%;"  -->


#### Course slides
* These slides
   ```
   git clone https://github.com/heytrav/sc-2018.git
   ```
   <!-- .element: style="font-size:12pt;"  -->
* Install nodejs and run the course slides
   ```
   cd ~/sc-2018/slides
   npm install
   npm start
   ```
* This should open a browser with the slides for this workshop


### Setup Docker

* Follow instructions on website for installing <!-- .element: class="fragment" data-fragment-index="0" -->
   * [Docker Community Edition](https://store.docker.com/search?offering=community&type=edition)
   * [docker-compose](https://docs.docker.com/compose/install/)
* If you are using Ubuntu, you can use the ansible playbook included in course repo <!-- .element: class="fragment" data-fragment-index="1" -->

```
cd docker-introduction
ansible-galaxy -f -r ansible/requirements.yml
ansible-playbook -i ansible/hosts -K ansible/docker-install.yml 
```
<!-- .element: class="fragment" data-fragment-index="1" -->


#### Installing Docker
* Check which version of Docker you have
   ```
   docker --version
   ```


#### Installing `docker-compose`
* Check which version of `docker-compose` is installed
   ```
   docker-compose --version
   ```

#### Checkout code for workshop
* Example voting app
   ```
   git clone https://github.com/docker/example-voting-app.git
   ```
   <!-- .element: style="font-size:10pt;"  -->
* Ansible for setting up Kubernetes
   ```
   git clone https://github.com/heytrav/k8s-ansible.git
   ```
   <!-- .element: style="font-size:12pt;"  -->
* Follow [README](https://github.com/heytrav/k8s-ansible) instructions for
  setting up environment
