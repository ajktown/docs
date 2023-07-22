# aws-load-balancer-controller

<!-- TOC -->

- [aws-load-balancer-controller](#aws-load-balancer-controller)
  - [Overview](#overview)
  - [Why](#why)
  - [How to install](#how-to-install)

<!-- /TOC -->

## Overview

`AWS Load Balancer Controller` is AWS officially supported customized controller that watches your ingress deployment and automatically creates and configures the application load balancer on AWS.

It also watches the deletion of ingress and deletes the load balancer once the ingress is deleted.

## Why

Instead of creating your own managed reverse proxy, you can simply use the `AWS Load Balancer Controller` to create and manage the load balancer for you.

We highly recommend to install `aws-load-balancer-controller` before you deploy any applications on the EKS clsuter.

## How to install

Follow this [AWS official documentation](https://docs.aws.amazon.com/eks/latest/userguide/aws-load-balancer-controller.html) to install the controller.