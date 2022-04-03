# Secrets

- A built-in feature of kubernetes
- External vault services (like `hashicorp's vault`) can also be used
- Secrets can be injected to a service both as env variable or as a file
- Secrets in manifest file (`kind: Secret`), data should be base64 encoded

## Creating and Reading Secrets

- Create secret: `kubectl -f create ../resources/3-secret.yml`
- Create a deployment and mount secrets a as volume: `kubectl create -f ../resources/4-deployment-with-secrets.yml`
- Get one of the pod name: `kubectl get pods`
- Connect one of the pod: `kubectl exec -ti <pod-name> -- /bin/sh`
- Validate that the credentials have been stored in `/etc/creds`. It will be read-only
- Validate that the credentials have been stored as env variable
```
echo $USERNAME
echo $PASSWORD
```
