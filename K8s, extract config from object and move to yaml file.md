If we want to modify a pod, we will need to delete and then define it a again via yaml or imperative. 
```
kubectl get pod webapp-color -o yaml >> pod.yaml
```
We can then open that file, edit and run a
```
kubect apply -f pod.yaml
```
