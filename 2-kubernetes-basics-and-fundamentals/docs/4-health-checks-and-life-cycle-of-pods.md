# Health Checks and Life Cycle of Pods

Using Deployment resource a set of pods and their lifecycles can be smoothly managed.

- It runs a command in the container `periodically`
- the command makes an HTTP request to a specified URL
- A typical production ready application should always have health checks implemented for the sake
  of availability and resilliency.
- There are two types of health checks
    1. livenessProbe
    2. readinessProbe

## Deploying a Set of Pods with Health Checks

- `kubectl create -f ../resources/2-deployment-with-health-check-liveness-probe.yml`
- check pods: `kubectl get pods` 
- describe one of the pod and check `Conditions` section: `kubectl describe pod <pod-name>`
- While `Deployment` resource is trying to download and run the the image, `readinessProbe` waits
  15 seconds and makes a request to `localhost:8080/version`. If response status code is 200 then
  the pods' state will be ready.
- terminate the deployment: `kubectl delete deployment simple-go-api-with-liveness-probe`

## Health Check with readinessProbe

- `livenessProbe` indicates whether a container is running, if the checks fails, the container(s)
  will be restarted
- `readinessProbe` indicates whether pod(s) are `ready to serve` requests
- If the check fails, the container will not be restarted, but pod's IP address will be removed
  from the service, so it will not serve any requests anymore
- When test succeeded, then the pod will receive requests
