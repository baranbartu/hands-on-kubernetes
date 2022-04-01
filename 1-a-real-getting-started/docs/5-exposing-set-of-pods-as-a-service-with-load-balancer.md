# Exposing Deployment as Service (LoadBalancer)

Previously, we exposed a deployment as NodePort service, which means each node in the cluster in
the service can be accessed using any node's IP (in this case it was minikube) and node port. Node
port can be seen with `kubectl get service hello-minikube -o yaml` under `spec.ports.nodePort`. If
port is explicitly defined in [manifest](../resources/2-exposing-pods-as-service-with-node-port.yml)
it will be assigned as node port. If not, kubernetes will assign a port itself.

Now we will expose service with LoadBalancer which means each service will have its own address to
the internet. This is the standard way to expose a service to the internet. In any cloud that has
load balancer support will provide a load balancer and we are going to do this example in later
steps. Now, we are going to focus `minikube`

When `kubectl get service hello-minikube -o wide` we will see `EXTERNAL-IP` for the service. If
`minikube`, it will by default be `pending` or `null` but we will make minikube to assign an
external IP adress by tunneling.


Run below commands to expose the [same deployment](../resources/1-single-replica-pod-deployment.yml) that we previously exposed as [NodePort](../resources/2-exposing-pods-as-service-with-node-port.yml) to
expose as `LoadBalancer` this time.

- `minikube tunnel` (It will make minikube cluster to assign an EXTERNAL-IP) when service is
  exposed.
- `kubectl create -f ../resources/3-exposing-pods-as-service-with-load-balancer.yml`
- Check if new service (hello-minikube-load-balancer) has an external ip: `kubectl get services -o wide`

> When service type is `LoadBalancer`, a CLUSTER-IP and a nodePort is also assigned, which means,
> we can also use internal cluster ip and node port to access the cluster. But since we already
> have done this previously, this time we will be using the external ip to access the service.
