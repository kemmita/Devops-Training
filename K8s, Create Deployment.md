Create file deployment.yaml
```
apiVersion: apps/v1
kind: Deployment
metadata:
  name: erste-app-deployment # name of deployment
spec:
  replicas: 2 # number of pods to start
  selector:
    matchLabels:
      app: erste-app
  template: # anything related to pod configuration lives within the template body below
    metadata:
      labels:
        app: erste-app
    spec:
      containers: # container(s) specs listed below for the pod(s)
        - name: erste-node-app
          image: kemmitr/k8-erste-app
```

Then run command to apply the deployment.
```
kubectl apply -f=deployment.yaml
```
