### Developing Microservices


#### Developing Applications
* Applications can consist of many components <!-- .element: class="fragment" data-fragment-index="0" -->  ![basic cluster](img/prod-application.svg "Simple Application") <!-- .element: class="img-right" style="width:30%;" -->
   * Web server (nginx, apache)
   * Database (sql, nosql)
   * Message Queue 
   * Your application
* <!-- .element: class="fragment" data-fragment-index="1" -->Typically spread across cluster of machines 


#### Single VM Development

* Often desireable for dev to be similar to production environment <!-- .element: class="fragment" data-fragment-index="0" -->
* In practice this is often difficult to achieve  <!-- .element: class="fragment" data-fragment-index="1" -->
   * Limited CPU of dev machines <!-- .element: class="fragment" data-fragment-index="2" -->![dev-env](img/dev-prod-deploy.svg "Dev environment") <!-- .element: class="img-right fragment" style="width:40%;" data-fragment-index="4" -->
   * Cost of machines <!-- .element: class="fragment" data-fragment-index="3" -->
* Compromise is to develop everything in single VM <!-- .element: class="fragment" data-fragment-index="4" --> 



#### Pitfalls of Single VM Development
* Single VM development creates blindspot <!-- .element: class="fragment" data-fragment-index="0" -->
* Developers can make false assumptions about <!-- .element: class="fragment" data-fragment-index="1" -->
   * Which config files on which machines <!-- .element: class="fragment" data-fragment-index="2" -->
   * Which dependency libraries present on machines <!-- .element: class="fragment" data-fragment-index="3" -->
* Difficult to scale individual services <!-- .element: class="fragment" data-fragment-index="4" -->
* Applications components often tightly coupled <!-- .element: class="fragment" data-fragment-index="5" -->
* Can lead to unpredictable behaviour when application is deployed to production <!-- .element: class="fragment" data-fragment-index="6" -->


#### Containers to the rescue
* Containers can make this easier <!-- .element: class="fragment" data-fragment-index="0" -->
* Container serves as the  <!-- .element: class="fragment" data-fragment-index="1" -->_unit_ equivalent of microservice
* Deployable artefact (i.e. <!-- .element: class="fragment" data-fragment-index="2" -->_image_)
* Can be versioned <!-- .element: class="fragment" data-fragment-index="3" -->
* Layered filesystem <!-- .element: class="fragment" data-fragment-index="4" -->
   + Deploying updates equivalent of deploying _just what was changed_
Note: containers mitigate some of the above issues


#### Using containers in development
* So how can we run a containerised application in development?
* <!-- .element: class="fragment" data-fragment-index="0" -->`docker-compose`
   + A tool for easily bootstrapping multi-container applications
   + i.e. microservice
   + Ideal for developing/testing applications on a workstation
* Let's create an application using <!-- .element: class="fragment" data-fragment-index="1" -->`docker-compose`


#### Exercise: Create microservices `docker-compose`
```
 cd ~/kubernetes-microservices-workshop/sample-code/mycomposeapp 
```
<!-- .element: class="fragment" data-fragment-index="0" -->
* Let's build a simple application with two components <!-- .element: class="fragment" data-fragment-index="1" -->
   * Web application using Python Flask
   * Redis message queue
* The app is already in mycomposeapp/app.py <!-- .element: class="fragment" data-fragment-index="2" -->
* We want to run the app and redis as separate microservices <!-- .element: class="fragment" data-fragment-index="3" -->
* Redis is already available as a <!-- .element: class="fragment" data-fragment-index="4" -->[docker image](https://hub.docker.com/_/redis/)


#### Create Our App
* Fire up your favourite editor and create a Dockerfile <!-- .element: class="fragment" data-fragment-index="0" -->
   - For example
   ```
   vim Dockerfile
   ```
   <!-- .element: style="font-size:13pt;"  -->
* Add the following contents to <!-- .element: class="fragment" data-fragment-index="1" -->`Dockerfile`
   ```
   FROM python:3.7-alpine
   WORKDIR /code
   COPY requirements.txt /code
   RUN pip install -r requirements.txt
   COPY . /code
   CMD ["python", "app.py"]
   ```


#### Writing a docker-compose file
* In the same directory as previous example <!-- .element: class="fragment" data-fragment-index="0" -->
* Create a file called <!-- .element: class="fragment" data-fragment-index="1" -->`docker-compose.yml`
* Add our service definition: <!-- .element: class="fragment" data-fragment-index="2" -->
   ```
  ---
  version: "3"
  services:
    web: 
      build: .
      ports: 
        - "5000:5000"
    redis:
      image: redis:alpine
   ```
 <!-- .element: style="font-size:10pt;" -->
* Start our microservices <!-- .element: class="fragment" data-fragment-index="3" -->
   ```
   docker-compose up -d
   ```
* Confirm application running at <!-- .element: class="fragment" data-fragment-index="4" -->[localhost:5000](http://localhost:5000)


#### What did `docker-compose` do?
* Check that services are running
   ```
   docker-compose ps
   ```
* Have a look at `docker-compose.yml`
* Compose created two services
   + _web_ - which automatically built using our `Dockerfile`
   + _redis_  - pulled from the official `redis:alpine`
* Port 5000 on host machine mapped to 5000 on _web_ service


#### Benefits of `docker-compose`
* Orchestration of containers (a.k.a _services_)
* Mount directories and _named volumes_
  - persistent storage for databases
  - local filesystem for development
* Additional features
  - create multiple networks
  - scale _services_
* A _production_ deployment platform?


#### Scaling Services
* Try scaling the redis service to 4 instances <!-- .element: class="fragment" data-fragment-index="0" -->
   ```
   docker-compose up -d --scale redis=4
   ```

<asciinema-player class="fragment" data-fragment-index="1" autoplay="1" loop="loop"  font-size="medium" speed="1"
     theme="solarized-light" src="asciinema/docker-compose-scaling-service.json"
     cols="138" rows="15"></asciinema-player>


#### Stopping `docker-compose`

* In the directory where your `docker-compose.yml` file is, run:
   ```
   docker-compose stop
   ```


#### Summary

* `docker-compose` provides useful way to setup development environments
* Takes care of
   * networking
   * linking containers
   * scaling services
