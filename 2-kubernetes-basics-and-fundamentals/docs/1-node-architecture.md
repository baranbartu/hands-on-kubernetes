# Node Architecture

- kubelet
- kube-proxy
- pod
- iptables
- node
- service


## Kubelet

Kubelet is responsible to launch pods. It talks to master node to get related information about
pod's state and keeps them run.

## Kube-proxy

kube-proxy feeds its information to `iptables` to make pods and services are accessible both within
the cluster and from outside of the cluster.

## Iptables

Whenever a new pod is launched, kube-proxy updates the iptables to make it accessible accross the
cluster.

## Pod

A pod is a single unit that can have multiple containers. And with composition of one or more
containers, it becomes a single application that is not ready for production yet. However, when a
set of pods are exposed through a service, pods will become a reliable service that has multiple
replicas.

## Node

Node represents an instance of kubernetes cluster that is not a `master` instance.

## Service

An abstract way to expose a set of pods to the cluster or/and outside as a service.
