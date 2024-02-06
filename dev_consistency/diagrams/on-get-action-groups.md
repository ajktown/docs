# On Get Action Groups

<!-- TOC -->

- [On Get Action Groups](#on-get-action-groups)
  - [Overview](#overview)

<!-- /TOC -->


TODO: Still Writing

## Overview

This is a basic diagram for onGetActionGroups, used when user wants to see the action groups. This is only for the owner's action group, which returns the action group details and the actions.

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
  user -> fe: User wants to see action groups
  activate fe
    fe -> api: GET /api/v1/action-groups
    activate api
      api -> db: Get Action Group Docs
      activate db
        api <- db: Return action group docs
      deactivate db
      break if action group is not owned by the user
        fe <- api: Return 403
      end break
      fe <- api: Return ActionGroupDomain.toRes() of all
      note right
        - level and count is fixed as 1 at this moment
      end note
    deactivate api
  deactivate fe
deactivate user
```