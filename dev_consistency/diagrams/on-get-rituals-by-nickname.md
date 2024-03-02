# On Get Rituals by Nickname

<!-- TOC -->

- [On Get Rituals by Nickname](#on-get-rituals-by-nickname)
  - [Overview](#overview)

<!-- /TOC -->

## Overview

Unlike `onGetRituals`, this sequence (`onGetRitualsByNickname`) includes public api that anyone can access to get rituals by nickname.


```plantuml

@startuml

title onGetRitualsByNickname()

participant "End User" as user

box "FE" #Lightblue
  participant "FE" as fe
box
box "API" #Lightgreen
  participant "API" as api
box

activate user
  user -> user: User wants to see ritual by nickname
  user -> fe: Goes to page consistency.ajktown.com/users/:nickname
  note right
    if user name is mlajkim
    URL => will be consistency.ajktown.com/users/mlajkim
  end note
  activate fe
    fe -> api: GET /api/v1/users/:nickname/rituals
    activate api
      note right
        As Mar 2, 2024, the ritual is not yet managed in the DB and has only default ritual.
        And therefore the current api simply gets all action groups and group them into the default ritual.
      end note
      api -> db: Get User by nickname
      activate db
        api <- db: Return user
      deactivate db
      break if user not found with such nickname OR user has not made their rituals public
        fe <- api: Returns 404
        note right
          For the privacy sake, you should not tell the details and just return 404
          The error message should be
          "No such user or the user has not make their rituals public."
        end note
        user <- fe: Tells user that there is no such user or not public
      end break
      api -> db: Get Action Group Docs
      activate db
        api <- db: Return action group docs
      deactivate db
      api -> api: Wrap every action group under the default ritual named "Unassociated Ritual"
      fe <- api: Return Ritual.toResShared() of every ritual
      note right
        This will filter out hidden action groups
        and only return the owner approved action groups.
      end note
    deactivate api
    user <- fe: Shows action groups under the rituals
  deactivate fe
deactivate user
```