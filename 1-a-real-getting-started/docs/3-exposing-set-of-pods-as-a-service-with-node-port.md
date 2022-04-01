# Exposing Deployment as Service

Kubernetes is ment to be an orchestration for bunch of services and their communication.
Previously, we reached to a single `Pod's` port. But in general, we'd have multiple `Pods` for an
application or service. A kubernetes' `Service` is an abstract way to expose an application running
on set of `Pods` as a network service. Thus, services can communicate each other, and services can
be accessible from outside with a neat way.

We can expose a set of `Pod` with 2 methods again, `imperative` and `declarative`.

- Option 1 - Imperative approach: `kubectl expose deployment hello-minikube --type=NodePort --port=80`
- Option 2 - Declarative approach: `kubectl create -f ../resources/2-exposing-pods-as-service-with-node-port.yml`

> Both command creates exactly the same resources.


## Understanding the Service Concept

### Service Types

There are 3 service types. `ClusterIP`, `NodePort` and `LoadBalancer`.

1. `ClusterIP`: Service has an internal IP address within the cluster that is accessible from other
pods. This is default type for service unless it is not explicitly configured.
2. `NodePort`: An internal IP address is again created which means type `NodePort` service also has 
a capability of `ClusterIP` type, but also each cluster node is exposed a PORT which means service
can be accessible from also outside using node IP address and nodePort.
3. `LoadBalancer`: Service is exposed to outside with the help of cloud provider's load balancer.
There is also a way to use this type in `minikube`. We are going to do both in later steps.


### Port Types

There is also one more thing that confuses developers which is the `port` concept.

First run this to see `ports`: `kubectl get service/hello-minikube -o yaml`

As you see there are `ports` section under `spec`.

1. `nodePort`: It is the exposed node port that is accessible through per node's IP address and
   this port.
2. `port`: It is the service port. Remember, a service is an abstract way to expose a set of pods
   as a service. This port can be used within the cluster using `CLUSTER-IP` and this port.
3. `targetPort`: It is the pod's port that the service routes requests to.


## Conclusion

We expose the service using node port, this node port receives traffic through node's IP address,
then service handles the traffic on its port, then it routes request to target port.
