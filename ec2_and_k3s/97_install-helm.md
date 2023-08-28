# Install helm



I have attached every policy to work on my behalf

## Install git
Git is required to install

```sh
sudo yum install git -y
```

## export path
```sh

echo 'export PATH=$PATH:/usr/local/bin' >> ~/.bashrc
source ~/.bashrc


```
## Install helm

```sh

curl https://raw.githubusercontent.com/helm/helm/main/scripts/get-helm-3 | bash


```

## Set cluster name

```sh

CLUSTER_NAME=$(hostname)
echo "CLUSTER_NAME: $CLUSTER_NAME"

```

## preinstall service account

```sh
kubectl create serviceaccount aws-load-balancer-controller -n kube-system

```
## install aws load balancer


```sh
helm repo add eks https://aws.github.io/eks-charts
helm repo list
helm repo update

helm install aws-load-balancer-controller eks/aws-load-balancer-controller -n kube-system --set clusterName=$CLUSTER_NAME --set serviceAccount.create=false --set serviceAccount.name=aws-load-balancer-controller

```

![successful_install_of_aws_load_balancer](./assets/successful_install_of_aws_load_balancer.png)


## To uninstall
have to relinsta


```sh

helm list -n kube-system
helm uninstall aws-load-balancer-controller -n kube-system

```