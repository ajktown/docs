# Post Archived Action Group API

<!-- TOC -->

- [Post Archived Action Group API](#post-archived-action-group-api)
  - [Overview](#overview)
  - [PostArchivedActionGroupBodyDTO](#postarchivedactiongroupbodydto)
    - [actionGroupId: string](#actiongroupid-string)
    - [message: string](#message-string)
  - [Diagram](#diagram)

<!-- /TOC -->


## Overview

When user no longer needs an action group, they can archive it. This is a sequence diagram for archiving an action group using the AJK Town API.


## PostArchivedActionGroupBodyDTO

### actionGroupId: string
The id of the action group to be archived

### message: string
The reason why the user is archiving the action group

## Diagram


```plantuml

@startuml

title POST /api/v1/action-groups/:id/archive

participant "User" as user

box "API" #Lightgreen
  participant "API" as api
box
box "DB" #Crimson
  participant "DB" as db
box

activate user
  user -> api: POST /api/v1/action-groups/:id/archive
  activate api
    api -> db: Gets archived doc for the action group id
    activate db
      api <- db: Returns archived doc
    deactivate db
    break if the archived doc exists
      user <- api: Returns 400 Bad Request: The action group is already archived
    end break
    api -> db: Creates a new archived doc with the group id & body
    activate db
      api <- db: Returns the new archived-action-group doc
    deactivate db
    user <- api: Returns 200 OK: The action group is archived
  deactivate api
deactivate user
```