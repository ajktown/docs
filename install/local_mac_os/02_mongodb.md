# Prepare MongoDB

<!-- TOC -->

- [Prepare MongoDB](#prepare-mongodb)
  - [Overview](#overview)
    - [Choose your password for your mongo db server](#choose-your-password-for-your-mongo-db-server)
    - [Run the new container with the downloaded image](#run-the-new-container-with-the-downloaded-image)
    - [See if container is created](#see-if-container-is-created)
    - [Install `Mongo DB Compass`](#install-mongo-db-compass)

<!-- /TOC -->

## Overview
Install MongoDB on your local machine

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

### See if container is created
```sh
docker container ls | grep mongo
```

### Install `Mongo DB Compass`

Mongo DB Compass is a UI integrated application for the connections to the `prod` or `dev` DB env.

Visit the website [here](https://www.mongodb.com/try/download/compass) and get the latest version






