***We can use the imperative approach to generate any k8s object yaml file teamplate.***

1. run the below command to get an example from the output
```
kubectl create <deployment, service, configmap> --help
```
2. Take the example and appen the below text to create a yaml file you can build off of.
```
kubectl create deployment  redis-deploy --image=redis --replicas=2 --namespace=dev-ns --dry-run=client -o yaml > redissss-deployment.yaml
```
