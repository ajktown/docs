# Install K3s

<!-- TOC -->

- [Install K3s](#install-k3s)
  - [Overview](#overview)
  - [Run as sudo](#run-as-sudo)
  - [Install & Check](#install--check)
  - [Kubectl Config to the K3s generated config](#kubectl-config-to-the-k3s-generated-config)
  - [Enable dok3scker service at AMI boot time & start](#enable-dok3scker-service-at-ami-boot-time--start)
  - [Install worker nodes and connect](#install-worker-nodes-and-connect)

<!-- /TOC -->

## Overview

Install K3s on the cluster

## Run as sudo

```sh
sudo bash
```


## Install & Check

```sh

curl -sfL https://get.k3s.io | sh -

```

Check

```sh

systemctl status k3s

```


## Kubectl Config to the K3s generated config

```sh
echo "export KUBECONFIG=/etc/rancher/k3s/k3s.yaml" >> ~/.bashrc
source ~/.bashrc
```

## Enable dok3scker service at AMI boot time & start


```sh
kubectl get nodes

```

## Install worker nodes and connect

This documentation does not include workers but you can create workers connected to master node with the tutorials [here](https://youtu.be/zSlRUMm36n8?feature=shared).




