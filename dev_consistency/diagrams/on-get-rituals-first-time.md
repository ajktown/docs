# On Get Rituals First Time

<!-- TOC -->

- [On Get Rituals First Time](#on-get-rituals-first-time)
  - [Overview](#overview)
  - [Diagram](#diagram)

<!-- /TOC -->

## Overview

Unlike [on-get-rituals](./on-get-rituals.md), the diagram specifically includes the situation where user is first time and default ritual has never been made yet.


## Diagram

```mermaid

sequenceDiagram
title: onGetRituals() for the first time user

actor user as User
box SkyBlue React - AJK Town
  participant fe as FE
end
box Green API - AJK Town
  participant api as API
  participant domain as RitualGroupDomain
end
box DarkRed mongodb - AJK Town
  participant db as DB
end


activate user
  user ->> fe: Opens ConsistencyGPT for the first time
  activate fe
    fe ->> api: GET /api/v1/rituals
    activate api
      api ->> domain: Runs RitualGroupDomain.fromReq()
      activate domain
        domain ->> db: Requests "action group docs" of the requester
        activate db
          db ->> domain: Returns empty list of "action group docs"
        deactivate db
        domain ->> domain: Considers it as a new user of ConsistencyGPT
        domain ->> db: Creates a default ritual named "Unassociated Ritual"
        activate db
          db ->> domain: Returns the newly created default ritual
        deactivate db
        domain ->> api: Returns itself
      deactivate domain
      api ->> fe: Returns RitualGroupDomain.toRes(actionGroupModel)
    deactivate api
    fe ->> user: Shows nothing as there is no action group under the default ritual
  deactivate fe
deactivate user
```