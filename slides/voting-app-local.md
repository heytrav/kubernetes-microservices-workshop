## Docker Workflow Example


### Example Voting Application

* Microservice application consisting of 5 components ![voting-app](img/voting-app.png "Voting App") <!-- .element: class="img-right" -->
    * Python web application <!-- .element: class="fragment" data-fragment-index="0" -->
    * Redis queue <!-- .element: class="fragment" data-fragment-index="1" -->
    * .NET worker <!-- .element: class="fragment" data-fragment-index="2" -->
    * Postgres DB with a data volume <!-- .element: class="fragment" data-fragment-index="3" -->
    * Node.js app to show votes in real time <!-- .element: class="fragment" data-fragment-index="4" -->


### Start Application
```
cd ~/example-voting-app
```
<asciinema-player autoplay="1" loop="loop"  font-size="medium" speed="1"
    theme="solarized-light" src="asciinema/docker-compose.json" cols="174" rows="15"></asciinema-player>
[Vote](http://localhost:5000) and [view results](http://localhost:5001)


### Interactive development

* Open up <code>vote/app.py</code> 
* On lines 8 & 9, modify vote options
* View change in <a href="http://localhost:5000">voting</a> application


### Change Vote Options
<asciinema-player autoplay="1" loop="loop"  font-size="medium" speed="1" theme="solarized-light" src="asciinema/asciicast-120556.json" cols="138" rows="21"></asciinema-player>


### Developer Workflow

* Push code to repository <!-- .element: class="fragment" data-fragment-index="0" -->
* Continuous Integration (CI) system runs tests <!-- .element: class="fragment" data-fragment-index="1" -->
* If tests successful, automate image build &amp; push to a docker registry <!-- .element: class="fragment" data-fragment-index="2" -->
* Easy to setup with existing services <!-- .element: class="fragment" data-fragment-index="3" -->
   * [DockerHub](https://hub.docker.com) (eg. [these slides](https://hub.docker.com/r/heytrav/docker-introduction-slides/builds/))
   * [GitHub](https://github.com)
   * [CircleCI](https://circleci.com)
   * GitLab
   * [Quay.io](https://quay.io)


### Developer Workflow

* Ship your artefact directly using docker-compose <!-- .element: class="fragment" data-fragment-index="0" -->
   * Useful if you want to test an image immediately
* Tell docker-compose to rebuild the image <!-- .element: class="fragment" data-fragment-index="1" -->
* Let's build and tag the image as <!-- .element: class="fragment" data-fragment-index="2" -->`YOURNAME/vote:v2` and push to [hub.docker.com](https://hub.docker.com)
* This will come in handy in an example we're doing later <!-- .element: class="fragment" data-fragment-index="2" -->
```
docker-compose build vote
docker tag examplevotingapp_vote:latest YOURNAME/vote:v2
docker push YOURNAME/vote:v2
```
<!-- .element: class="fragment" data-fragment-index="2" -->


### Summary

* With docker-compose it's relatively easy to develop on a microservice application
* Changes visible in real time
* Can easily package and distribute images for others to use
