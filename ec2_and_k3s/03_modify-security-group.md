# AWS Security Group

<!-- TOC -->

- [AWS Security Group](#aws-security-group)
  - [Overview](#overview)
  - [Modify Security Group](#modify-security-group)

<!-- /TOC -->

## Overview

AWS Security Group must be modified to allow HTTP and HTTPS traffic to the instance.


## Modify Security Group


| Type  | Port | Source        |
|:------|:-----|:--------------|
| HTTP  | 80   | 0.0.0.0 (All) |
| HTTPS | 443  | 0.0.0.0 (All) |