```
apiVersion: v1
kind: Service
metadata:
  name: erste-app-service # name of service
spec:
  selector:
    app: erste-app # name of pod(s) to target, pod was created during the deployment
  ports:
    - protocol: 'TCP'
      port: 80 # external port to access from the browser
      targetPort: 8080 # internal port
  type: LoadBalancer # this will expose it to the outside world
```

Run command
```
kubectl apply -f=service.yaml
```
