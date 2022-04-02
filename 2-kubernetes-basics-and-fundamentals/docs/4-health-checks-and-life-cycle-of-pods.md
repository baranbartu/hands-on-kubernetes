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

- `kubectl create -f ../resources/2-deployment-with-health-check-readiness-probe.yml`
- check pods: `kubectl get pods` 
- describe one of the pod and check `Conditions` section: `kubectl describe pod <pod-name>`
