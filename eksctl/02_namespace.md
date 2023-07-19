
# namespace setup

<!-- TOC -->

- [namespace setup](#namespace-setup)
  - [Overview](#overview)
  - [How](#how)
    - [imperative command](#imperative-command)
    - [yaml file](#yaml-file)

<!-- /TOC -->

## Overview

You can organize your application within the same namespace in k8s.

Namespace must be created before applying other k8s resources like `Deployment`, `Service`, `Ingress` etc.

## How

You can use either imperative command or yaml file.


### imperative command

```sh
kubectl create namespace ajktown
```


### yaml file

```yaml
apiVersion: v1
kind: Namespace
metadata:
  name: ajktown
```

then apply

```sh
kubectl apply -f namespace.yaml
```