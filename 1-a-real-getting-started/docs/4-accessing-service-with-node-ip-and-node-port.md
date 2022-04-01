# Accessing the Service

Since we exposed the service using `NodePort`, the service now is accessible with both
(CLUSTER-IP - service port) and (node ip - nodePort) pairs


## Accessing the Service with CLUSTER-IP and Service Port

Regardles of the service type, which is in this case `NodePort`, an internal `CLUSTER-IP` for the
service is always assigned and can be used internally within the cluster. In this case, accessing
port should be spec.ports.port which is the internal service port.

- Get service's internal IP: `kubectl get service hello-minikube --output='jsonpath="{.spec.clusterIP}"'`
- Get service internal port: `kubectl get service hello-minikube --output='jsonpath="{.spec.ports[0].port}"'`
- SSH to minikube: `minikube ssh`
- `curl <internal-ip>`:<service-port>

> Service port can also be seen in the resource [file](../resources/2-exposing-pods-as-service-with-node-port.yml)

> Exactly same method can also be used in another service within the cluster. We can basically
> access this service from another service or pod by using cluster ip and service port.


## Accessing the Service with Node IP and Node Port

- Get minikube ip (a.k.a node ip): `minikube ip`
- Get node port: `kubectl get service hello-minikube --output='jsonpath="{.spec.ports[0].nodePort}"'`
- Or we can directly call instead of above two: `minikube service hello-minikube`

> Apple M1 users might face an issue for accessing the service using node ip especially when docker
> driver us used. But this commands will give the proper access in intel chips, or any linux
> device. 


## Accessing the Service With Service Port Forwarding

1. Get service port: `kubectl get service hello-minikube --output='jsonpath="{.spec.ports[0].port}"'`
1. Forward `service's` port to a local port: `kubectl port-forward service/hello-minikube 8001:<service-port>`
2. Make request from your local: `curl -X GET "localhost:8001?foo=bar"`
``
