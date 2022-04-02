# Services In Details

In the first section (getting started), we already mentioned quickly about exposing services. But
here we are going to talk about it a bit more.

- Pods are dynamic, they die and lives over and over again
- That's why pods should not be accessed directly, but always through a service
- Service is a bridge between pods and other services or end-users
- Creating a service will create an endpoint for the pod(s)
    - ClusterIP: Virtual IP address that is only reachable within the cluster
    - NodePort: A same port in each node is exposed externally
    - LoadBalancer: The ultimate way to expose a service to outside. This will route
                    external traffic to every node on the NodePort
- By default, a service can only run between ports (30000 - 32767) but it can be
  configured
