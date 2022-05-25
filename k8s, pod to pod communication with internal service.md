1. We have an auth API that we want to reference internally, let's create an auth deployment.
```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: auth-deployment
spec:
  replicas: 1
  selector:
    matchLabels:
      app: auth
  template:
    metadata:
      labels:
        app: auth
    spec:
      containers:
        - name: auth
          image: kemmitr/auth-network-example:latest
```
2. Now let's create a service to expose the auth service internally to the cluster
```yaml
apiVersion: v1
kind: Service
metadata:
  name: auth-service
spec:
  selector:
    app: auth
  type: ClusterIP
  ports:
    - protocol: TCP
      port: 80
      targetPort: 80
```
3. Now we can reference the IP / URL in any application deployment we choose.
```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: users-deployment
spec:
  replicas: 1
  selector:
    matchLabels:
      app: users
  template:
    metadata:
      labels:
        app: users
    spec:
      containers:
        - name: users
          image: kemmitr/user-network-example:latest
          # Below we create an env var that our src code can reference
          env:
            - name: AUTH_ADDRESS
              value: "auth-service.default" # the name of th service defined on line 26 and the namespace it is housed in "default"
```
