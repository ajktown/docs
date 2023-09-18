# Install K3s



## Overview


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




