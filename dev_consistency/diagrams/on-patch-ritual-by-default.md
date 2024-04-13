# On Patch Ritual By Id

<!-- TOC -->

- [On Patch Ritual By Id](#on-patch-ritual-by-id)
  - [Overview](#overview)
  - [Modifiable Attributes](#modifiable-attributes)
  - [Diagram](#diagram)

<!-- /TOC -->

## Overview
Sequence diagram for patching properties of the default `default ritual`.

Only `default ritual` exists as of Apr 2024.

This is due to the fact that we only support one ritual per user.

`"PATCH  /api/v1/rituals/default"` only.

## Modifiable Attributes

As of Apr 2024, the only modifiable attribute is `orderedActionGroupIds`.

## Diagram

```mermaid

sequenceDiagram
title: onPatchRitualByDefaultId()

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
  user ->> fe: Changes order of ActionGroups for the default ritual id
  activate fe
    fe ->> api: Requests PATCH /api/v1/rituals/default
    Note right of fe: DTO contains action_group_ids
    activate api
      api ->> domain: Runs RitualGroupDomain.patch(dto)
      activate domain
        domain ->> db: Requests "ritual" docs of the requester
        activate db
          db ->> domain: Returns ritual (As of Apr 2024, we only support one ritual per user)
        deactivate db
        domain ->> domain: Knows the default ritual id
        domain ->> db: Requests update the default ritual based on given PatchRitualGroupBodyDTO
        activate db
          db ->> domain: Updates and returns the updated ritual doc
        deactivate db
        domain ->> domain: Stores the action groups under the default ritual
        domain ->> domain: Sorts action groups based on the orderedActionGroupIds of RitualDomain props
        domain ->> api: Returns itself
      deactivate domain
      api ->> fe: Returns RitualGroupDomain.toRes()
    deactivate api
    fe ->> user: Shows modified order of the action groups, as the ritual's `orderedActionGroupIds` is updated
  deactivate fe
deactivate user
```