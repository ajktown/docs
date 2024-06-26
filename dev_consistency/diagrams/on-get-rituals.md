# On Get Rituals

<!-- TOC -->

- [On Get Rituals](#on-get-rituals)
  - [Overview](#overview)
  - [GetRitualsQueryDTO](#getritualsquerydto)
    - [isArchived: boolean](#isarchived-boolean)
  - [Diagram](#diagram)

<!-- /TOC -->

## Overview

Ritual contains action groups and each action group manages its own actions.

RitualGroupDomain will smartly create a new default ritual if the user does not have any rituals yet.

## GetRitualsQueryDTO

### isArchived: boolean
  - If true, it will return only archived action groups
  - If false, it will return only non-archived action groups
  - If undefined, it will return all action groups whether archived or not

## Diagram
```mermaid

sequenceDiagram
title: onPatchRitualById()

actor user as User
box SkyBlue React - AJK Town
  participant fe as FE
end
box Green API - AJK Town
  participant api as API
  participant domain as RitualGroupDomain
  participant ritual_domain as RitualDomain
end
box Crimson mongodb - AJK Town
  participant db as DB
end


activate user
  user ->> fe: Get rituals of the user
  activate fe
    fe ->> api: Requests GET /api/v1/rituals
    activate api
      api ->> domain: Runs RitualGroupDomain.fromMdb()
      activate domain
        domain ->> db: Requests "ritual" docs of the requester
        activate db
          db ->> domain: Returns ritual (As of Apr 2024, we only support one ritual per user)
        deactivate db
        domain ->> db: Requests "archived_action_groups" docs of the requester
        activate db
          db ->> domain: Returns archived_action_groups
        deactivate db
        domain ->> db: Requests "action group" docs of the requester
        activate db
          db ->> domain: Returns "action group" docs
        deactivate db
        domain ->> domain: Stores the action groups under the default ritual
        Note right of domain: action groups under archived_action_groups are filtered out
        domain ->> domain: Sorts action groups based on the orderedActionGroupIds of RitualDomain props
        domain ->> api: Returns itself
      deactivate domain
      api ->> fe: Returns RitualGroupDomain.toRes()
    deactivate api
    fe ->> user: Shows nothing as there is no action group under the default ritual
    Note right of user: Users before "Rituals" schema (Before Mar 20, 2024) <br/>will have the newly created ritual with their original action groups
  deactivate fe
deactivate user
```
