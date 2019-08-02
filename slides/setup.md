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
   + minikube
* Training machines should be setup <!-- .element: class="fragment" data-fragment-index="1" -->
   + Ubuntu (xenial)
* Following slides contain instructions for setting up environment <!-- .element: class="fragment" data-fragment-index="2" -->



#### Install some dependencies
* [Docker Community Edition](https://store.docker.com/search?offering=community&type=edition)
* [docker-compose](https://docs.docker.com/compose/install/)
* [minikube](https://kubernetes.io/docs/tasks/tools/install-minikube/)
  + [virtualbox](https://www.virtualbox.org/wiki/Downloads)

Note: some of these should be done anyway but you might have to walk through
them anyway



#### Course slides
* Check that your environment contains following directories
  - kubernetes-microservices-workshop
  - example-voting-app
* Run the course slides <!-- .element: class="fragment" data-fragment-index="2" -->
   ```
   cd ~/kubernetes-microservices-workshop/slides
   npm start
   ```
   <!-- .element: style="font-size:12pt;"  -->
* This should open a browser with the slides for this workshop <!-- .element: class="fragment" data-fragment-index="3" -->
