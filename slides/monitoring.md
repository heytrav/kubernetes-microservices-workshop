### Monitoring


#### Monitoring Kubernetes
* Large applications can be difficult to keep tabs on
   - running services
   - resource usage
   - across dynamic set of pods, nodes
* Important to consider monitoring at the beginning of any project
* Alerting when something goes wrong
* Lots of tools available for this


#### Common Monitoring Tools
* [Graphite](https://graphite.readthedocs.org/en/latest)
* [InfluxDB](https://influxdata.com)
* [OpenTSDB](https://opentsdb.net)
* [Nagios](https://www.nagios.org)
* [Prometheus](https://prometheus.io)


#### Prometheus
* Full monitoring and trending system with built in scraping, storage and
  alerting
* Time series data identified by metric and key/value pairs
* Flexible query langugage
* Open source 
* Part of the CNCF since 2016 



#### Integrating Prometheus

* Change directories to the prometheus operator repository
   ```
   cd ~/prometheus-operator/contrib/kube-prometheus
   ```
* Apply manifests
   ```
   kubeptl create -f manifests/ || true
   ```
* Check that things are up and running
   ```
   kubeptl -n monitoring get all
   ```
   ```
    NAME                                       READY   STATUS    RESTARTS   AGE
    pod/alertmanager-main-0                    2/2     Running   0          1h
    pod/alertmanager-main-1                    2/2     Running   0          1h
    pod/alertmanager-main-2                    2/2     Running   0          1h
   ```
   <!-- .element: class="fragment" data-fragment-index="0" -->


#### Prometheus Architecture ![Prometheus architecture](img/prometheus-architecture.png "Prometheus Architecture") <!-- .slide: class="image-slide" -->


#### Monitoring
* In the previous slide we did several things 
* First we created a new _monitoring_ namespace
* Then we kicked off a bunch of new pods and services in this namespace
   * Prometheus
   * alert managers
   * Grafana
* At the moment we have no way to visualise these services


#### Visualising our Monitoring
* Open up a new terminal
* Set up port forwarding for Grafana
   ```
   kubeptl -n monitoring port-forward \
       svc/grafana 3000
   ```
* Now open [Grafana](http://127.0.0.1:3000) in your browser
* User password `admin/admin` 


#### Visualise the Alert Manager
* Open up a new terminal
* Set up port forwarding for the alert manager
   ```
   kubeptl -n monitoring port-forward  \
       svc/alertmanager-main 9093
   ```
* No open the [alert manager](http://127.0.0.1:9093) in your browser


##### Summary
* It is important to monitor your Kubernetes cluster
* Tools exist for doing this
   * Prometheus
* We'll continue to check on this as we interact with our cluster
