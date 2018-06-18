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


#### Checkout code for workshop
* These slides
   ```
   git clone ..../scaleconf-workshop-2018.git
   ```
* Example voting app
   ```
   git clone https://github.com/docker/example-voting-app.git
   ```
* Ansible for setting up Kubernetes
   ```
   git clone https://github.com/heytrav/k8s-ansible.git
   ```



#### Course slides
* Install nodejs and run the course slides
   ```
   cd ~/scaleconf-workshop-2018/slides
   npm install
   npm start
   ```
* This should open a browser with the slides for this workshop


#### Install some dependencies
* Docker
* `docker-compose`
* `minikube`
* Ansible


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


#### Installing and Setup Ansible
* Create and activate a Python virtual environment
   ```
   virtualenv -p /usr/bin/python2 $WORKDIR/venv
   source $WORKDIR/venv/bin/activate
   ```
* Install libraries required for Ansible and lesson
   ```
   (venv) pip install -r $WORKDIR/requirements.txt
   ```
