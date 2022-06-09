1. Create secret
```
kubectl create secret generic my-secret --from-literal=key1=supersecret --from-literal=key2=topsecret -o yaml >> test_secret.ya
ml
```
2. Edit and update file
```yaml
apiVersion: v1
data:
  key1: c3VwZXJzZWNyZXQ=
  key2: dG9wc2VjcmV0
kind: Secret
metadata:
  creationTimestamp: "2022-06-09T18:52:29Z"
  name: my-secret
  namespace: default
  resourceVersion: "203589"
  uid: 91b5d2c5-56ad-4050-a615-8bd32f7ea118
type: Opaque
```
3. apply
```
kubectl apply secret.yaml
```
4. reference secrets in deployment/pods
```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  labels:
    app: html-deployment
  name: html-deployment
spec:
  replicas: 1
  selector:
    matchLabels:
      app: html-deployment
  template:
    metadata:
      labels:
        app: html-deployment
    spec:
      containers:
      - image: kodekloud/webapp-color
        imagePullPolicy: Always
        name: color
        envFrom:
          - secretRef:
              name: my-secret
        resources: {}
```
