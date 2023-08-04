# Install Kubectl


<!-- TOC -->

- [Install Kubectl](#install-kubectl)
  - [Overview](#overview)
  - [Install Kubectl](#install-kubectl-1)
  - [Check installed kubectl](#check-installed-kubectl)
  - [Reference](#reference)

<!-- /TOC -->

## Overview


## Install Kubectl


```sh

# This is arm64 kubectl
curl -LO "https://dl.k8s.io/release/$(curl -L -s https://dl.k8s.io/release/stable.txt)/bin/linux/arm64/kubectl"
chmod +x ./kubectl
mkdir -p $HOME/bin && cp ./kubectl $HOME/bin/kubectl && export PATH=$HOME/bin:$PATH
echo 'export PATH=$HOME/bin:$PATH' >> ~/.bashrc


```
https://kubernetes.io/docs/tasks/tools/install-kubectl-linux/

## Check installed kubectl


```sh

kubectl version --output=yaml

```

![kubectl_installed](./assets/kubectl_installed.png)


## Reference

- https://docs.aws.amazon.com/eks/latest/userguide/install-kubectl.html
- https://crishantha.medium.com/running-minikube-on-aws-ec2-e845337a956
