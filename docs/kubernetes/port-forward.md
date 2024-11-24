---
sidebar_position: 2
---

# Port forward

To forward certain resource in the K8s server to your local machine we can follow the general rule:

```shell
kubectl port-forward <resource_type>/<resource_name> <host_port>:<resource_port>
```

## Service

```shell
kubectl port-forward svc/myservice 8090:8080
```
