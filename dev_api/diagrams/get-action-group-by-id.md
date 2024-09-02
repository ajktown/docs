# Get Action Group By Id

<!-- TOC -->

- [Get Action Group By Id](#get-action-group-by-id)
  - [Overview](#overview)
  - [Diagram](#diagram)

<!-- /TOC -->

## Overview
Endpoint `GET /api/v1/action-groups/{id}` is used to get the details of an action group with the id.
ㅁ

## Diagram

```plantuml
@startuml


title GET /api/v1/action-groups/{id}


participant "User" as user

box "API" #Lightgreen
  participant "API" as api
box

activate user
  user -> api: GET /api/v1/words/{id}
  activate api
    break if given id is ActionGroupFixedId.DailyPostWordChallenge
      user <- api: ActionGroupDomain.fromWordChunk()
    end break
    user <- api: ActionGroupDomain.fromId()
  deactivate api
deactivate user
```