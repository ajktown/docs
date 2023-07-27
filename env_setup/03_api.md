# Env Setup

<!-- TOC -->

- [Env Setup](#env-setup)
  - [Overview](#overview)
  - [Purpose](#purpose)
    - [Copy .env.local.sample into .env.local](#copy-envlocalsample-into-envlocal)
    - [Prepare env value](#prepare-env-value)
    - [Apply generated env value to .env](#apply-generated-env-value-to-env)
    - [Install packages](#install-packages)
    - [Run API Server](#run-api-server)

<!-- /TOC -->

## Overview
You will set up env data for api application of ajktown project.

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

### Apply generated env value to .env

```sh
vi ~/ajktown/.env
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