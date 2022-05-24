1. Creat config map
```
apiVersion: v1
kind: ConfigMap
metadata:
  name: env-store
data:
  folder: 'story'
```
2. Apply to cluster
```
kubectl apply -f=environment.yaml
```
3. Update deployment file
```
apiVersion: apps/v1
kind: Deployment
metadata:
  name: story-deployment
spec:
  replicas: 2
  selector:
    matchLabels:
      app: story
  template:
    metadata:
      labels:
        app: story
    spec:
      containers:
        - name: story
          image: kemmitr/story
          env:
            # Below is the name that you will reference in your src code to obtain the value
            - name: STORY_FOLDER
              valueFrom:
                configMapKeyRef:
                  # Below is the name of the config map we defined above.
                  name: env-store
                  $ below is the value you obtain from the configMap using the key name
                  key: folder
          volumeMounts:
            - mountPath: /app/story # this is specified in the Dockerfile WORKDIR /app and in the src code of the app
              name: story-volume
      volumes:
        - name: story-volume
          hostPath:
            path: /data # path of the dir that lives on the VM that houses the cluster->node->pod
            type: DirectoryOrCreate
```
3. Update your deployment with the apply command
