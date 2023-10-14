# Share Feature


<!-- TOC -->

- [Share Feature](#share-feature)
  - [Overview](#overview)
  - [General Flow](#general-flow)

<!-- /TOC -->

## Overview

Share feature is basically share your word card with others by generating SharedResourceDomain.


## General Flow

```plantuml

@startuml

title Share Word Id Flow

participant "End User" as user
participant "FE" as fe
box "API" #Lightgreen
  participant "API Gateway" as api
  participant "API Middleware" as mdl
  participant "AccessTokenDomain" as atd
  participant "API Controller" as ctl
box
activate user
  user -> fe: User clicks the share button
  activate fe
    fe -> fe: Opens A dialog with loading indicator
    fe -> api: Sends API Request POST /api/v1/shared-resource
    activate api
      api -> api: TODO: Write stuff
      fe <- api: TODO: Do something
    deactivate api
  fe -> fe: Copies the generated URL to clipboard of the end user.
  fe -> fe: The loading indicator disappears
  user <- fe: Tells the user that the URL is copied to clipboard
  deactivate fe
  user -> user: User has the link that can be shared with others
deactivate user


```