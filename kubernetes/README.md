# FAQ

## How do you override a file on a pod?
Check out [configmap](/configmap) folder for example
<details>
  <summary>Click for summary</summary>
  
  1. Create a configmap file

```yaml
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

## How do you mount a configmap as a file?
<details>
  <summary>Click for summary</summary>
  
  1. Create a configmap file

```yaml
 ...
data:
  config:
    settings.yaml: |-
      your yaml file here
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
      - mountPath: <directory path>/settings.yaml
        subPath: settings.yaml
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

## How do I pull a private docker image?
Check out [secrets](/secrets) folder for example
<details>
  <summary>Click for summary</summary>

  1. Run the following command to create a docker registry secret

```bash
kubectl create secret docker-registry <name of secret> --docker-server="<docker registry url>" --docker-username="<docker username" --docker-password="<docker password" --docker-email="<docker email>"
```

  2. And imagePullSecrets config to your yaml file.

```yaml
...
spec:
  imagePullSecrets:
  - name: <name of secret>
```
</details>

## How do I add labels to namespace and nodes on openshift?

Node label:
```
oc label node node1.ubuntu.local app=nodejs
```

Namespace label:
```
oc edit ns ${project name}
```
Then add the label under **metadta** > **annotations**
```
openshift.io/node-selector: app=ocgocd
```
