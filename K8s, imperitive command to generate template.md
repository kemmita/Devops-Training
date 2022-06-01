The below command will generate a template for a deployment so that we do not need to create one from scratch.
```
kubectl create deployment redis-deploy --image=redis --replicas=2 --namespace=dev-ns --dry-run=client -o yaml > redissss-deployment.yaml
```
