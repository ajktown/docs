# On Post Action Group

<!-- TOC -->

- [On Post Action Group](#on-post-action-group)
  - [Overview](#overview)

<!-- /TOC -->

TODO: Still Writing

## Overview
This is a basic diagram for onPostActionGroup. This is used when user wants to post a new action group for their newly goal of consistency.


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
  user -> fe: Clicks "create" to post action group
  note right
    name: name of the action group
  end note
  activate fe
    fe -> api: POST /api/v1/action-group
    activate api
      api -> db: Create Action Group
      note right
        The same name is permitted for the same user.
        - Time standard: UTC
        - Number of allowed commits: 1
      end note
      activate db
        api <- db: Return action group
      deactivate db
      fe <- api: Return created action group
    deactivate api
    user <- fe: Shows created action group
  deactivate fe
deactivate user
```