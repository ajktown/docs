# On Post Action

<!-- TOC -->

- [On Post Action](#on-post-action)
  - [Overview](#overview)

<!-- /TOC -->

TODO: Still Writing

## Overview
This is a basic diagram for onPostAction, used when user has contributed.


```plantuml

@startuml

title usePostActionGroup()

participant "End User" as user

box "FE" #Lightblue
  participant "FE" as fe
box
box "API" #Lightgreen
  participant "API" as api
box

activate user
  user -> fe: User commits into consistency as an action
  activate fe
    fe -> api: POST /api/v1/action
    note right
      - id: id of the action group (must)
    end note
    activate api
      api -> db: Get Action Group Docs
      activate db
        api <- db: Return action group docs
      deactivate db
      break if action group is not owned by the user
        fe <- api: Return 403
      end break
      break if number of actions for the data range of the action group
        note right
          The first beta phase will only allow one action per day.
          The first beta phase will only allow the UTC time.
        end note
        fe <- api: Return 400
      end break
      api -> db: Create Action
      activate db
        api <- db: Return action
      deactivate db
      fe <- api: Return ActionGroupDomain.toRes()
    deactivate api
  deactivate fe
deactivate user
```