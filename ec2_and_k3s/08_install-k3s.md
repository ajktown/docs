# Install K3s



## Overview




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

Check

```sh
kubectl get nodes

```



