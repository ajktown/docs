# Api Setup

<!-- TOC -->

- [Api Setup](#api-setup)
  - [Overview](#overview)
  - [Purpose](#purpose)
    - [Copy .env.local.sample into .env.local](#copy-envlocalsample-into-envlocal)
    - [Double check your MDB_PASSWORD](#double-check-your-mdb_password)
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

### Double check your MDB_PASSWORD

```sh
echo "MDB_PASSWORD: $MDB_PASSWORD"
# MDB_PASSWORD: local_root_XXXXXXXXXXXXXXXXXXXXXXXXXXXX
```

if it prints nothing for MDB_PASSWORD, please set up MDB_PASSWORD [here](./01_clone-projects.md#choose-your-password-for-your-mongo-db-server).


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