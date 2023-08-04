# EC2 and Minikube

<!-- TOC -->

- [EC2 and Minikube](#ec2-and-minikube)
  - [Overview](#overview)
  - [Connect to the EC2 with EIP attached](#connect-to-the-ec2-with-eip-attached)

<!-- /TOC -->

## Overview

Connect to the EC2 with EIP attached

## Connect to the EC2 with EIP attached

Do the following command to connect to EC2 instance on Terminal[^1]
```sh

cd /to/where/your/minikube-ec2-ajktown.pem/is/located/at
sudo ssh -i "minikube-ec2-ajktown.pem" ec2-user@ec2-54-238-235-29.ap-northeast-1.compute.amazonaws.com

```

[^1]: Highly recommend to alias the command above for future use so that you can simply do the following command
  ```sh
    ajktown-ec2
  ```