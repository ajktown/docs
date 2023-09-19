# AWS Security Group

<!-- TOC -->

- [AWS Security Group](#aws-security-group)
  - [Overview](#overview)
  - [Modify Security Group](#modify-security-group)

<!-- /TOC -->

## Overview

AWS Security Group must be modified to allow HTTP and HTTPS traffic to the instance.


## Modify Security Group


| Type  | Port | Source        | Description                        |
|:------|:-----|:--------------|:-----------------------------------|
| HTTP  | 80   | 0.0.0.0 (All) | Allow HTTP traffic from anywhere   |
| HTTPS | 443  | 0.0.0.0 (All) | Allow HTTPS traffic from anywhere  |
| SSH   | 22   | YOUR_IP       | Your Home IP or work place IP only |