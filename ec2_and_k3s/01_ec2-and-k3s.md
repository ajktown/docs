# EC2 and K3s

<!-- TOC -->

- [EC2 and K3s](#ec2-and-k3s)
  - [Overview](#overview)
  - [Estimated Price](#estimated-price)
  - [Prerequisite Knowledge](#prerequisite-knowledge)

<!-- /TOC -->

## Overview

Although you can simply deploy your application with eksctl like the instruction we provide [here](eksctl/01_setup.md), the price of EKS is not cheap. This instruction will let you use simple EC2 instance and k3s to deploy your application.

## Estimated Price

Total $16 per month

Calculation
- t4g.small = $0.0216 per hour * 24 hours * 30 days = $15.552 (or $16)
- ALB, EBS and other services are free tier

## Prerequisite Knowledge
- AWS
  - VPC
  - EC2
- Bash
