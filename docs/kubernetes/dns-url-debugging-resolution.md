---
sidebar_position: 1
---

# DNS|URL debugging resolution

Often I need to verify connection from Pods to Services and understand why they seem not to be able to talk to each other. We can use DNS debugging and also basic CURL commands for it.

## DNS debugging

- Deploy a pod that has `nslookup` installed:

```shell
cat << EOF | kubectl apply -f -
apiVersion: v1
kind: Pod
metadata:
  name: dnsutils
spec:
  containers:
  - name: dnsutils
    image: registry.k8s.io/e2e-test-images/agnhost:2.39
    imagePullPolicy: IfNotPresent
    command:
      - /bin/sh
      - -c
      - "sleep 3600"
  restartPolicy: Always
EOF
```

- Use the pod created to starting verifying whether or not Services are reachable:

```shell
kubectl exec -it dnsutils -- nslookup kubernetes.default
```

> Replace `kubernetes.default` by the service you are trying to test. E.g. `my_service.namespace.svc:8080`

## CURL debugging

- Deploy a pod that has `curl` installed:

```shell
cat << EOF | kubectl apply -f -
apiVersion: v1
kind: Pod
metadata:
  name: alpine-curl
spec:
  containers:
  - name: alpine-curl
    image: docker.io/alpine/curl:latest
    imagePullPolicy: IfNotPresent
  restartPolicy: Always
EOF
```

- Use the pod created to starting verifying whether or not Services are reachable:

```shell
kubectl exec -it alpine-curl -- curl https://google.com
```
