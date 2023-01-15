# reloader
reloader is a tool that tracks changes in configmaps and reloads the pods as needed 
add 
```yaml 
kind: Deployment
metadata:
  annotations:
    reloader.stakater.com/auto: "true"
```
to your deployment file and reloader will take care of the rest.
