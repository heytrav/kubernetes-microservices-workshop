### Monitoring


#### Monitoring Kubernetes
* Large applications can be difficult to keep tabs on
   - running services
   - resource usage
   - across dynamic set of pods, nodes
* Alerting when something goes wrong
* Important to consider monitoring at the beginning of any project
* Lots of tools available for this


#### Prometheus
* Open source 
* Time series data identified by metric and key/value pairs


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
   kubeptl -n monitoring port-forward svc/grafana 3000
   ```
* Now open [Grafana](http://127.0.0.1:3000) in your browser


#### Visualise the Alert Manager
* Open up a new terminal
* Set up port forwarding for the alert manager
   ```
   kubeptl -n monitoring port-forward svc/alertmanager-main 9093
   ```
* No open the [alert manager](http://127.0.0.1:9093) in your browser


##### Summary
* It is important to monitor your Kubernetes cluster
* Tools exist for doing this
   * Prometheus
* We'll continue to check on this as we interact with our cluster
