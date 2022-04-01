# Decommissioning Existing Resources

```
kubectl delete service hello-minikube-load-balancer
kubectl delete service hello-minikube

# with below command, pods are going to be removed as well
kubectl delete deployment hello-minikube

kubectl delete pod busybox
```
