

# DNS Setup

<!-- TOC -->

- [DNS Setup](#dns-setup)
  - [Overview](#overview)
  - [How to set up (Google Domain)](#how-to-set-up-google-domain)
  - [Check if DNS is successfully pointed](#check-if-dns-is-successfully-pointed)

<!-- /TOC -->

## Overview

We are going to set up DNS that should point to AWS ALB for final exposure to the world.

User => DNS => ALB => Ingress => Service => Pod

## How to set up (Google Domain)


go to `https://domains.google.com`

Click your domain

![click_domain](./assets/click_domain.png)

Click DNS
![click_dns](./assets/click_dns.png)

Click Manage Custom Records
![click_manage_custom_records](./assets/click_manage_custom_records.png)

Add your AWS Load Balancer (ALB) DNS and save
![add_alb_dns](./assets/add_alb_dns.png)


## Check if DNS is successfully pointed

![check_if_dns_set_up_successfully](./assets/check_if_dns_set_up_successfully.png)