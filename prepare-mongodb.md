# Prepare MongoDB

<!-- TOC -->

- [Prepare MongoDB](#prepare-mongodb)
  - [Overview](#overview)
  - [Instructions](#instructions)
    - [Get the latest image from the Docker server](#get-the-latest-image-from-the-docker-server)
    - [Set your new Mongo DB Password](#set-your-new-mongo-db-password)
    - [Create mongo DB image with settings](#create-mongo-db-image-with-settings)
    - [See if container is created](#see-if-container-is-created)
    - [Install `Mongo DB Compass`](#install-mongo-db-compass)

<!-- /TOC -->

## Overview

Basic tutorial of setting up Mongo DB Image locally so that your AJK Town API can be connected to Local API

## Instructions

Source: https://medium.com/@szpytfire/setting-up-mongodb-within-a-docker-container-for-local-development-327e32a2b68d

### Get the latest image from the Docker server
```sh
docker pull mongo
```

### Set your new Mongo DB Password
```sh
MDB_PASSWORD="local_root_71aae4225232353a9736957210416f22d8571c"
echo "SAVED_MDB_PASSWORD: $MDB_PASSWORD"
```

### Create mongo DB image with settings
```sh
docker run -d --name mongodb -p 27017 \
-e MONGO_INITDB_ROOT_USERNAME=root \
-e MONGO_INITDB_ROOT_PASSWORD="${MDB_PASSWORD}" \
mongo 

```


### See if container is created
```sh
docker container ls | grep mongo
```

### Install `Mongo DB Compass`

Mongo DB Compass is 

Visit the website [here](https://www.mongodb.com/try/download/compass) and get the latest version


