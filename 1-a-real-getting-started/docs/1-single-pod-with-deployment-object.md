# Creating Pods

We need to create `Pod(s)`. There is a couple of ways to do that. `Kind` attribute of resource
manifest file can be `Pod`, `ReplicaSet` and `Deployment` in order to run `Pod(s)`.
Eventually each does the same thing in a different way, but `Deployment` is the best-practise
to enable running `Pod(s)` in Kubernetes.


## Creating Pod(s) using Deployment Object

We are going to create kubernetes `Pod(s)` using Deployment` object. There are two ways,
`imperative` and `declarative`. We are going to try both. But declarative approach is the best
practice. We are going to do both, pick one or try both in order to test it.

- Option 1 - Create kubernetes resources with `imperative` approach:
```
kubectl create deployment hello-minikube --image=ealen/echo-server --port=80 --replicas=1
```
- Option 2 - Create kubernetes resources with `declarative` approach:
```
kubectl create -f ../resources/1-single-replica-pod-deployment.yml
```
- Validate `Deployment`, `ReplicaSet` and `Pod` resources:
```
kubectl get deployments
kubectl get replicasets
kubectl get pods
```

Both method do the same thing on kubernetes. Create one `Deployment` resource which keeps the
ultimate state of our Pod, Pod's aliveness and count are managed by `ReplicaSet` which was
created by the `Deployment` resource. We always have one running `Pod` at a time with this conf.

> NOTE: We created `Pods` `Deployment` resource but we did not expose it as a service. We just have
> Pod(s) at the moment. It means that we can only access to a single container at a time using
> Pod's private IP and port.
