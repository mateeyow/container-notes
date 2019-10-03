# FAQ

## Building image in docker-compose

```yaml
version: '3'

serviceName:
  build:
    context: <path of your dockerfile "." if its the same path>
```

## How do I mount docker folder or files to the container

```bash
docker run -v /path/to/your/file.txt:/path/to/your/container/file.txt -v /path/to/folder:/path/to/folder image-name
```
