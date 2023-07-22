# aws-load-balancer-controller

<!-- TOC -->

- [aws-load-balancer-controller](#aws-load-balancer-controller)
  - [Overview](#overview)
  - [How to install](#how-to-install)

<!-- /TOC -->

## Overview

`AWS Load Balancer Controller` is AWS officially supported customized controller that watches your ingress deployment and automatically creates and configures the application load balancer on AWS.

It also watches the deletion of ingress and deletes the load balancer once the ingress is deleted.


## How to install

Follow this [AWS official documentation](https://docs.aws.amazon.com/eks/latest/userguide/aws-load-balancer-controller.html) to install the controller.