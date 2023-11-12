# Install plantuml


<!-- TOC -->

- [Install plantuml](#install-plantuml)
  - [Overview](#overview)
  - [Prerequisites](#prerequisites)
    - [Sample Plantuml Code](#sample-plantuml-code)
  - [Basic installs](#basic-installs)
    - [Install PlantUML extension if not installed](#install-plantuml-extension-if-not-installed)
  - [Run Locally](#run-locally)
    - [Run plantuml docker image locally](#run-plantuml-docker-image-locally)
    - [Set local setting](#set-local-setting)
    - [Enable loading content over http served from localhost](#enable-loading-content-over-http-served-from-localhost)
  - [Run Remotely](#run-remotely)
    - [Set remote setting](#set-remote-setting)

<!-- /TOC -->

## Overview
How to install plantuml and test


## Prerequisites
- What is Plantuml?
  - `Plantuml` is a component that allows you to quickly write: Sequence diagram · Usecase diagram · Class diagram · Object diagram · Activity diagram (Detailed information [here](https://plantuml.com/))
  - You can run it locally, or remotely


### Sample Plantuml Code
You can do `command + shift + v` to see the preview of the flow below:
```plantuml

@startuml

title Handshaking between FE and API

participant "Frontend (FE)" as fe
participant "API Server" as api

activate fe
  fe -> api: Hi, API!
  activate api
    fe <- api: Hello, FE!
  deactivate api
deactivate fe

```

## Basic installs
Basic installs contain the shared install for both local and remote

### Install PlantUML extension if not installed
![install_vscode_plantuml](./assets/install_vscode_plantuml.png)

## Run Locally
Pros
- You can secure your plantuml code by not sending it to 3rd party remote server

Cons
- Requires docker to be running

### Run plantuml docker image locally
```
docker run -d -p 12000:8080 plantuml/plantuml-server:jetty
```

### Set local setting
**open setting**
```
command + shift + v
```
![open_setting](./assets/open_setting.png)


**set local plantuml setting**
![setting](./assets/plantuml-server-setting.png)


### Enable loading content over http served from localhost
![enable_loading_content_over_localhost](./assets/enable_loading_content_over_localhost.png)



## Run Remotely
Pros
- Does not require remote server

Cons
- Requires internet connection
- Your data will be sent to plantuml
- Generally slower

### Set remote setting
**open setting**
```
command + shift + v
```
![open_setting](./assets/open_setting.png)

**set remote plantuml setting**
![set_remote_plantuml_server](./assets/set_remote_plantuml_server.png)