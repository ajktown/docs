# Env Setup

<!-- TOC -->

- [Env Setup](#env-setup)
  - [Overview](#overview)
  - [Purpose](#purpose)
    - [Copy .env.local.sample into .env.local](#copy-envlocalsample-into-envlocal)
    - [Prepare env value](#prepare-env-value)
    - [Install packages](#install-packages)
    - [Run API Server](#run-api-server)

<!-- /TOC -->

## Overview
step by step

## Purpose
Although every step might be possibly wrong as the time passes, it gives a general idea of how to set up the environment.


### Copy .env.local.sample into .env.local

```sh
cd ~/ajktown/api
cp .env.local .env
```

### Prepare env value

```sh
echo "MDB_LOCAL_URI=mongodb://root:${MDB_PASSWORD}@localhost:57017/?authSource=admin"
echo "JWT_TOKEN_SECRET=$(openssl rand -base64 32)"
```

### Install packages
```sh
# In yarn, $ yarn == $ yarn install
yarn
```

### Run API Server

```sh
yarn dev 
```