# FAQ

## Building image in docker-compose

```yaml
version: '3'

serviceName:
  build:
    context: <path of your dockerfile "." if its the same path>
```