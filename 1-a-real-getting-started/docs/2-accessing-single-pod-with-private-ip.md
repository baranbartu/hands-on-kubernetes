# Accessing a Single Pod

> NOTE: Assuming that the previous step is done.

Without a `Service`, `Pod(s)` can only be accesible within the cluster. Each `Pod` has its own
private IP and it is accessible within the cluster. We are going to reach the `echo-server` by
using a couple of different ways.


## Accessing the Container Using Pod's localhost

1. Get pod name: `POD_NAME=$(kubectl get pods| grep hello-minikube| awk '{print $1}')`
2. Login the pod: `kubectl exec -ti $POD_NAME -- /bin/sh`
3. Make request from inside the container:
```
apk add curl
curl localhost:80?foo=bar
```

## Accessing the Container Using Another Pod

1. Get Pod's private IP: `POD_PRIVATE_IP=$(kubectl get pod $POD_NAME --output='jsonpath="{.status.podIP}"'| sed -e 's/^"//' -e 's/"$//')`
2. Run another pod with `busybox` image: `kubectl run --env="POD_PRIVATE_IP=$POD_PRIVATE_IP" -i -t busybox --image=busybox --restart=Never -- sh`
3. Try telnet to other pod using it's private IP address and container's port:
```
telnet $POD_PRIVATE_IP 80
GET /?foo=bar
# press ENTER again
```

## Accessing the Container By Logging in to Minikube's Node

1. Login to `minikube` node: `minikube ssh`
2. Make request using Pod's private address and container's port again: `curl <private-ip-of-node>:80?foo=bar`

## Accessing the Container with Port Forwarding

1. Forward `Pod's` port to a local port: `kubectl port-forward pod/$POD_NAME 8003:80`
2. Make request from your local: `curl -X GET "localhost:8003?foo=bar"`


> Make sure that you finalized all above steps successfully before moving forward!

## Conclusion

Pod can contain multiple containers, all containers wihin the pod share the same internal network
which is also the `localhost` of `Pod`. And Pod's port (while deploying) should be equal the
`Container's` exposed port.
That's why container's exposed port should be equal to `--port` argument in `imperative` cli command
or the `containerPort` attribute inside the `1-single-replica-pod-deployment.yml` manifest file 
while `Deployment` object is created.
