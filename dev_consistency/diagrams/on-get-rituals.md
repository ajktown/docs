# On Get Action Groups

<!-- TOC -->

- [On Get Action Groups](#on-get-action-groups)
  - [Overview](#overview)

<!-- /TOC -->

## Overview

Ritual contains action groups and each action group manages its own actions.


```plantuml

@startuml

title onGetRituals()

participant "End User" as user

box "FE" #Lightblue
  participant "FE" as fe
box
box "API" #Lightgreen
  participant "API" as api
box

activate user
  user -> fe: User wants to see rituals
  activate fe
    fe -> api: GET /api/v1/rituals
    activate api
      note right
        As Mar 2, 2024, the ritual is not yet managed in the DB and has only default ritual.
        And therefore the current api simply gets all action groups and group them into the default ritual.
      end note
      api -> db: Get Action Group Docs
      activate db
        api <- db: Return action group docs
      deactivate db
      api -> api: Wrap every action group under the default ritual named "Unassociated Ritual"
      fe <- api: Return Ritual.toRes() of every ritual
    deactivate api
    user <- fe: Shows action groups under the rituals
  deactivate fe
deactivate user
```