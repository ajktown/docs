# Env Setup

<!-- TOC -->

- [Env Setup](#env-setup)
  - [Overview](#overview)
  - [Purpose](#purpose)
    - [Install docker](#install-docker)
    - [Choose your password for your mongo db server](#choose-your-password-for-your-mongo-db-server)
    - [Run the new container with the downloaded image](#run-the-new-container-with-the-downloaded-image)
    - [Creae a directory for ajktown project](#creae-a-directory-for-ajktown-project)
    - [Clone Projects](#clone-projects)
    - [Copy .env.local.sample into .env.local](#copy-envlocalsample-into-envlocal)
    - [Install packages](#install-packages)
    - [Run Frontend](#run-frontend)

<!-- /TOC -->

## Overview
This is a step by step tutorial to set up the environment for ajktown project.
You will be cloning projects, installing packages, set environment variables, and run ajktown applications on your local machine.

## Purpose
Although every step might be possibly wrong as the time passes, it gives a general idea of how to set up the environment.


### Install docker

Go https://www.docker.com

And install docker


### Choose your password for your mongo db server

This instruction will build mongodb run on your local machine, and mongodb requires password to connect.
You need to choose your password for your mongodb server.

```sh
# i.e) MDB_PASSWORD="local_root_put_your_password_here"
MDB_PASSWORD="local_root_XXXXXXXXXXXXXXXXXXXXXXXXXXXX"
echo "SAVED_MDB_PASSWORD: $MDB_PASSWORD"
```

### Run the new container with the downloaded image

This will pull image mongodb from docker hub and run it on your local machine, with the password you set above. (or `MDB_PASSWORD`)

```sh
docker run -d --name mongodb -p 57017:27017 \
-e MONGO_INITDB_ROOT_USERNAME=root \
-e MONGO_INITDB_ROOT_PASSWORD="${MDB_PASSWORD}" \
mongo 
```

### Creae a directory for ajktown project

```sh
mkdir ~/ajktown
```

### Clone Projects


```sh
cd ~/ajktown
git clone https://github.com/ajktown/docs.git
git clone https://github.com/ajktown/wordnote.git
git clone https://github.com/ajktown/api.git
```


### Copy .env.local.sample into .env.local


```sh
cd ~/ajktown/wordnote
cp .env.local.sample .env.local
```

### Install packages
```sh
# In yarn, $ yarn == $ yarn install
yarn
```
### Run Frontend

```sh
yarn dev 
```