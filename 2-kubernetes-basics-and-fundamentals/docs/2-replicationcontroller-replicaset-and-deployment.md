# ReplicationController, ReplicaSet And Deployment

Three of them is kind of similar in order to manage pods and keep them alive based on rules.
But there is couple of slightly different usages and one of them is the best practise when it
comes to manage pods.


## ReplicationControler and ReplicaSet

Both do the same thing but `ReplicaSet` is a next generation `ReplicationController` that supports
both equality based selector and set based selector while `ReplicationController` only supports
equality based selector mechanism.

```
apiVersion: v1
kind: ReplicationController
metadata: 
  name: nginx-rc
spec:
  replicas: 3
  selector:
    app: nginx
    tier: dev
  template: 
    metadata:
      name: nginx
      labels: 
        app: nginx
        tier: dev
    spec:
      containers:
      - name: nginx-container
        image: nginx
        ports:
        - containerPort: 80
```
 
As you've seen `selector` works only for equality (`app: nginx`) based.

However, `ReplicaSet` is a bit superior when it comes to selector.

```
apiVersion: apps/v1
kind: ReplicaSet
metadata: 
  name: nginx-rs
spec:
  replicas: 3
  selector:
    matchLabels:
      env: prod
    matchExpressions:
    - { key: tier, operator: In, values: [frontend] }
  template:
    metadata:
      name: nginx
      labels: 
        env: prod
        tier: frontend
    spec:
      containers:
      - name: nginx-container
        image: nginx
        ports:
        - containerPort: 80
```

As you've seen there is also set based `matchExpressions` under `selector` and it makes
`ReplicaSet` a bit superior.

## Deployment

Deployment resource is the one that is most common and best practice. Because with `Deployment`, a
`ReplicaSet` is also created under the hood and rolling updates become much more easier whereas
with only `ReplicaSet` deploying a new version is more costly. We are going to use `Deployment`
resource most of the time.

- Start minikube if it is not working: `minikube start`
- Create `Deployment` resource alongside with `ReplicaSet` that will automatically keeps pods run:
    `kubectl create -f 1-two-replicas-pod-deployment.yml`
- Wait a bit and validate that pods are running: `kubectl get pods`
- We won't expose a service ATM, so just connect one of the pods: `kubectl exec -ti <pod-name> -- /bin/sh`
- Install curl: `apk add curl`
- Make a request: `curl localhost:8080/version` -> validate that the response contains `v1`

### Updating API Version During Runtime

Deployment resources make updating API versions really easier. We are going to update image
version to v2.

`kubectl edit deployment simple-go-api`

With above command, we will see that the existing pods will be terminated and new pods with
new version will be deployed by `ReplicaSet`

`kubectl get pods`

Wait a bit until new pods are deployed.

Then connect to one of the new pods and make a request to see response now contains `v2`

`kubectl exec -ti <pod-name> -- /bin/sh`

```
apk add curl
curl localhost:8080/version
```

If everything works properly so far, then we can terminate all the resources we created during this
playbook.

`kubectl delete deployment simple-go-api`
