### Setting up


#### Training Environment
* Training machines
   + Ubuntu 18.04?
   + Ubuntu 14.04


#### Checkout code for workshop
* These slides
* Example voting app



#### Course slides
* Repository for workshop should be on your machine
   ```
   cd ~/scaleconf-workshop-2018/slides
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
