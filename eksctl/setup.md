# eksctl setup


## Overview

eksctl is a simple CLI tool for creating clusters on EKS - Amazon's new managed Kubernetes service for EC2. It is written in Go, and uses CloudFormation.

eksctl is explained in a straightforward manner in [this video](https://youtu.be/p6xDCz00TxU).


## Install eksctl

## Check your default region of AWS

eksctl uses your aws configured region on ~/.aws/config

``` sh
$ cat ~/.aws/config
# Output:
# [default]
# region = ap-northeast-1
```

If you do not change your region, you have to specify region for every command.

``` sh
eksctl get clusters --region ap-northeast-1
```

## Change your region so that you do not have to specify region for every command

## Create Cluster

Creating a cluster takes about 10+ minutes
```sh
eksctl create cluster \
  --name test-cluster \
  --region ap-northeast-1 \
  --node-type t2.micro
```

## Get Cluster
```sh
eksctl get cluster
```

# Delete Cluster
Deleting a cluster takes about 5+ minutes
```sh
eksctl delete cluster --name test-cluster
```