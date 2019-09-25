# FAQ

## How do you override a file on a pod?
Check out [configmap](/configmap) folder for example
<details>
  <summary>Click for summary</summary>
  
  1. Create a configmap file

```javascript
 ...
data:
  config: |-
    your text here
```

  2. Map this configmap file to your deployment file
  
```yaml
...
spec:
  containers:
  - name: <your docker app>
    image: <your docker image>
    ports:
    - containerPort: <port>
    volumeMounts:
      - mountPath: <directory path>
        name: <name of volume>
  volumes:
  - name: <name of volume>
    configMap:
      name: <name of configmap>
      items:
      - key: <key of the configmap>
        path: <filename>
```
</details>
