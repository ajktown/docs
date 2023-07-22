# eksctl setup

<!-- TOC -->

- [eksctl setup](#eksctl-setup)
  - [Overview](#overview)
  - [Tips](#tips)
  - [Install eksctl](#install-eksctl)
  - [Check your default region of AWS](#check-your-default-region-of-aws)
  - [Requirements for instance](#requirements-for-instance)
  - [Create cluster with node type](#create-cluster-with-node-type)
    - [Create Cluster (ARM)](#create-cluster-arm)
    - [Create Cluster  (x86)](#create-cluster--x86)
  - [Get Cluster](#get-cluster)
- [Delete Cluster](#delete-cluster)

<!-- /TOC -->

## Overview

eksctl is a simple CLI tool for creating clusters on EKS. It will create separate vpc, security groups etc for your sake. 

eksctl is explained in a straightforward manner in [this video](https://youtu.be/p6xDCz00TxU).

## Tips 

If something does not go well as it is supposed to, I highly recommend to [delete cluster](#delete-cluster) and [create it again](#create-cluster-with-node-type).

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

We highly recommend to modify the region using `vi`
```sh
$ vi ~/.aws/config
```

## Requirements for instance

|   size    |                     remarks                     | Recommend? |
|:---------:|:-----------------------------------------------:|:----------:|
| t4g.micro |         barely handles. Very unstable.          |     No     |
| t4g.small | handles 1 pod each for api and wordnote[^1][^2] |    Yes     |

[^1]: Also supports 2 pods for rolling update
[^2]: Also supports 2 pods of aws-load-balancer-controller


## Create cluster with node type

If you build your image with arm architecture, you can use `t4g family`[^3].

If you build your image with x86 architecture, you can use `t2 family`[^3].

[^3]: You may use similar family for the next generation of instance type


### Create Cluster (ARM)
```sh
eksctl create cluster \
  --name ajktown-arm-cluster \
  --region ap-northeast-1 \
  --node-type t4g.small
```

### Create Cluster  (x86)

Creating a cluster takes about 10+ minutes
```sh
eksctl create cluster \
  --name ajktown-x86-cluster \
  --region ap-northeast-1 \
  --node-type t2.micro
```

## Get Cluster
```sh
eksctl get cluster
# $ eksctl get cluster
# NAME			          REGION		      EKSCTL CREATED
# ajktown-cluster-arm	ap-northeast-1	True
```

# Delete Cluster
Deleting a cluster takes about 5+ minutes
```sh
eksctl delete cluster --name <your-cluster-name>
```