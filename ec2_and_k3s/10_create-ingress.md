# Create Ingress

<!-- TOC -->

- [Create Ingress](#create-ingress)
  - [Overview](#overview)
  - [Ingress Controller](#ingress-controller)

<!-- /TOC -->

## Overview

Ingress is a service that allows you to access your service from outside the cluster.


## Ingress Controller

Since k3s is pre installed with Traefik, There is no need to install ingress controller.
You can simply apply your ingress.

```sh
kubectl apply -f your-ingress.yaml
```

