
# Get Words API

<!-- TOC -->

- [Get Words API](#get-words-api)
  - [Overview](#overview)
  - [Diagram](#diagram)

<!-- /TOC -->

## Overview
Sequence diagram for `AJK Town API` endpoint: `GET /api/v1/words`

## Diagram

```plantuml

@startuml

title GET /api/v1/words

participant "Requester" as user

box "API" #Lightgreen
  participant "API" as api
  participant "WordChunkDomain" as domain
box
database "MongoDB" as db

activate user
  user -> api: Request `GET /api/v1/words`
  activate api
    api -> api: Check authentication
    break if no authentication provided
      user <- api: Return 401 error (UnidentifiedUserError)
    end break
    api -> domain: Request list of WordDomains
    activate domain
      domain -> db: Request list of WordDocs
      activate db
        domain <- db: Return WordDocs
      deactivate db
      break if no WordDocs when requester's request only contains semester
        domain -> db: Deletes requester's semester from Supports.sems
        activate db
          domain <- db: Return OK
        deactivate db
      end break
      api <- domain: Return itself (WordChunkDomain)
    deactivate domain
    user <- api: Return WordChunkDomain.toResDTO()
  deactivate api
deactivate user
```
