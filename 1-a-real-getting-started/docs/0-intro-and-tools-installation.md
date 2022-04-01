# Introduction to Kubernetes

This guide is an easiest and the most efficient approach for introduction to Kubernetes.
Here, we are going to learn very basics with an efficient and short way.

We are going to create `Pod(s)` `resources` via `Deployment` `object` and expose this pod/container
as a `Service`. We are going to reach the `echo-server` with multiple ways like `minikube tunnel`,
`port-forwarding`, within the cluster/pod. We are going to cover port types `NodePort`, `Port`,
`TargetPort` and `Deployment` types `ClusterIp`, `NodePort` and `LoadBalancer`.

And we are going use `minikube`. At the end, understanding the overall concept is our primary aim.


## Minikube Installation

`minikube` can be installed by following [this](https://minikube.sigs.k8s.io/docs/start/) guidance
based on the OS you have.

Once you installed it, start it by running `minikube start`


## Kubectl Installation

`kubectl` can be installed by following [this](https://kubernetes.io/docs/tasks/tools/#kubectl)
guidance based on OS you have.

Verify te installation by running `kubectl`


## Some Basic Terms and Concepts

Kubernetes runs `Pods` that contains one or more containers, a set of `Pods` can be exposed as
`Service` to make the `service` accessible from other `Pods` and outside of the cluster.

We can manage `Pods` by using `Deployment`, `ReplicaSet` or `Pod` resource types. `Pod` is the main
focus but other type of resources are ment to manage the `Pod` resources.

Please check [this](https://kubernetes.io/docs/concepts/workloads/) for more information.
