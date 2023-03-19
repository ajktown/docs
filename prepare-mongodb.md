# Prepare MongoDB

<!-- TOC -->

- [Prepare MongoDB](#prepare-mongodb)
  - [Overview](#overview)
  - [Instructions](#instructions)
    - [Get the latest image from the Docker server](#get-the-latest-image-from-the-docker-server)
    - [Set your new Mongo DB Password](#set-your-new-mongo-db-password)
    - [Run the new container with the downloaded image](#run-the-new-container-with-the-downloaded-image)
    - [See if container is created](#see-if-container-is-created)
    - [Install `Mongo DB Compass`](#install-mongo-db-compass)

<!-- /TOC -->

## Overview

Basic tutorial of setting up Mongo DB Image locally so that your AJK Town API can be connected to Local DB

## Instructions

Source: https://medium.com/@szpytfire/setting-up-mongodb-within-a-docker-container-for-local-development-327e32a2b68d

### Get the latest image from the Docker server
You do not have to pull if you already have the mongo image, but the command below will allow you to update to the latest version of `mongo`.
```sh
docker pull mongo
```

### Set your new Mongo DB Password
```sh
MDB_PASSWORD="local_root_XXXXXXXXXXXXXXXXXXXXXXXXXXXX"
echo "SAVED_MDB_PASSWORD: $MDB_PASSWORD"
```

### Run the new container with the downloaded image

```sh
docker run -d --name mongodb -p 57017:27017 \
-e MONGO_INITDB_ROOT_USERNAME=root \
-e MONGO_INITDB_ROOT_PASSWORD="${MDB_PASSWORD}" \
mongo 

```

- 51514:27017
  - `27017` is the MongoDB standard port, and should not be modified unless you are super sure.
  - `57017` is the docker connection point, and you can customized whichever you want.
    - I simply set `57017` as it is similar number to the `27017`, so that I know that its for MongoDB.


### See if container is created
```sh
docker container ls | grep mongo
```

### Install `Mongo DB Compass`

Mongo DB Compass is a UI integrated application for the connections to the `prod` or `dev` DB env.

Visit the website [here](https://www.mongodb.com/try/download/compass) and get the latest version


