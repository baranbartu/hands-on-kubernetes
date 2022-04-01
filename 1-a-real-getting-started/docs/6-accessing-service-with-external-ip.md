# Accessing the Service

## Accessing With External IP

- Get the external IP of the new service: `kubectl get service hello-minikube-load-balancer -o wide` 
- Service Port is already `80` (We are not focusing the `nodePort`)
- Make request: `curl <EXTERNAL-IP>:<service port>`
