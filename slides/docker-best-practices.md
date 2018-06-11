## Designing Containerised Applications


### Developing Applications
* Applications can consist of many components <!-- .element: class="fragment" data-fragment-index="0" -->  ![basic cluster](img/prod-application.svg "Simple Application") <!-- .element: class="img-right" style="width:30%;" -->
   * Web server (nginx, apache)
   * Database (sql, nosql)
   * Message Queue 
   * Your application
* <!-- .element: class="fragment" data-fragment-index="1" -->Typically spread across cluster of machines 


### Development vs Production

* Ideal scenario: Development environment identical to production <!-- .element: class="fragment" data-fragment-index="0" -->
* In practice this is often difficult to achieve  <!-- .element: class="fragment" data-fragment-index="1" -->
   * Limited CPU of dev machines <!-- .element: class="fragment" data-fragment-index="2" -->![dev-env](img/dev-prod-deploy.svg "Dev environment") <!-- .element: class="img-right fragment" style="width:40%;" data-fragment-index="4" -->
   * Cost of machines <!-- .element: class="fragment" data-fragment-index="3" -->
   * Compromise is to develop everything in single VM <!-- .element: class="fragment" data-fragment-index="4" --> 


### Pitfalls of Single VM Development
* Single VM development creates blindspot <!-- .element: class="fragment" data-fragment-index="0" -->
* Developers can make false assumptions about <!-- .element: class="fragment" data-fragment-index="1" -->
   * Which config files on which machines <!-- .element: class="fragment" data-fragment-index="2" -->
   * Which dependency libraries present on machines <!-- .element: class="fragment" data-fragment-index="3" -->
* Difficult to scale individual services <!-- .element: class="fragment" data-fragment-index="4" -->
* Applications components often tightly coupled <!-- .element: class="fragment" data-fragment-index="5" -->
* Can lead to unpredictable behaviour when application is deployed to production <!-- .element: class="fragment" data-fragment-index="6" -->



### Misconception About Docker Containers

>I'll just put my entire application into a Docker container
> and run it that way

Common mistake to try and treat Docker containers like traditional VMs <!-- .element: class="fragment" data-fragment-index="0" -->


### Designing Containerised Applications
* Containerised application should <!-- .element: class="fragment" data-fragment-index="0" -->_smallest executable unit_
  * Have a single application <!-- .element: class="fragment" data-fragment-index="1" -->
  * Single executable runner <!-- .element: class="fragment" data-fragment-index="2" -->
  * Single process per container <!-- .element: class="fragment" data-fragment-index="3" -->
  * Single component of your application <!-- .element: class="fragment" data-fragment-index="4" -->
* No stored <!-- .element: class="fragment" data-fragment-index="5" -->_state_


### Containerise Application Components
* Each component is self-contained <!-- .element: class="fragment" data-fragment-index="0" -->![containerised-dev](img/containerised-dev-prod-deploy.svg "Containerised deploy") <!-- .element: class="img-right" style="width:50%;" -->
   * dependencies <!-- .element: class="fragment" data-fragment-index="1" -->
   * configuration <!-- .element: class="fragment" data-fragment-index="2" -->
* Better decoupling of components and dependencies <!-- .element: class="fragment" data-fragment-index="3" -->
* Brings us closer to production environment <!-- .element: class="fragment" data-fragment-index="4" -->



### Designing Containerised Applications
* Containerised component(s) should be agnostic to other services/components <!-- .element: class="fragment" data-fragment-index="0" -->
* Eg. application component may interact with <!-- .element: class="fragment" data-fragment-index="1" -->![agnostic](img/components-agnostic.svg "Agnostic Components") <!-- .element: class="img-right" -->
   * Containerised database in development  <!-- .element: class="fragment" data-fragment-index="2" -->
   * Cloud provider in production  <!-- .element: class="fragment" data-fragment-index="3" -->
    


### Something still not right
>Your Docker thingy still isn't <!-- .element: class="fragment" data-fragment-index="0" -->_exactly_ like production!

> Our application(s) are not deployed as Docker containers <!-- .element: class="fragment" data-fragment-index="1" -->


### Docker Developer Workflow
* In the following sections we'll explore ways of making development
  environment similar/identical to production <!-- .element: class="fragment" data-fragment-index="0" -->
* Development <!-- .element: class="fragment" data-fragment-index="1" -->
   * docker-compose as a tool for managing complex microservice applications in <!-- .element: class="fragment" data-fragment-index="2" -->
    development
* Production <!-- .element: class="fragment" data-fragment-index="3" -->
   * Orchestration platforms for deploying container workloads in production
     <!-- .element: class="fragment" data-fragment-index="4" -->
     environments
* Connecting the two with CI/CD workflows <!-- .element: class="fragment" data-fragment-index="5" -->
