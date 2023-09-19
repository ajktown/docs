# Install K9s

<!-- TOC -->

- [Install K9s](#install-k9s)
  - [Overview](#overview)
  - [Run as sudo](#run-as-sudo)
  - [Install](#install)
  - [Test if k9s is successfully installed](#test-if-k9s-is-successfully-installed)

<!-- /TOC -->
## Overview

Install K9s for easier management of K8s resources

## Run as sudo

```sh
sudo bash
```


## Install

```sh

curl -sS https://webinstall.dev/k9s | bash
source ~/.config/envman/PATH.env

```

## Test if k9s is successfully installed

```sh

k9s

```