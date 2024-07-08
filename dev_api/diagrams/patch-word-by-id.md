# Patch Word By Id

<!-- TOC -->

- [Patch Word By Id](#patch-word-by-id)
  - [Overview](#overview)
  - [Diagram](#diagram)

<!-- /TOC -->

## Overview
Endpoint `PATCH /api/v1/words/{id}` is used to update a word in the database. The user sends a request to the API with the word to be updated. The API then updates the word document in the database and returns the updated word document to the user.

## Diagram

```plantuml
@startuml


title PATCH /api/v1/words


participant "User" as user

box "API" #Lightgreen
  participant "API" as api
  participant "Word Service" as service
  participant "Word Domain" as domain
  participant "PreferenceDomain" as domain2
box
box "DB" #Crimson
  participant "DB" as db
box

activate user
  user -> api: PATCH /api/v1/words/{id}
  activate api
    api -> service: Get the word with the given word id
    activate service
      break if word does not exist
        api <- service: Returns 404 Not Found
        user <- api: Returns 404 Not Found
      end break
      api <- service: Returns the word domain
    deactivate service
    api -> domain: Request update with the request body
    activate domain
      break if owner of the word does not match to the requester's id
        api <- domain: Return 403 Forbidden; Requester does not have permission to update the word
      end break
      break if new tags are added
        domain -> domain2: Requests update for recentTags
      end break
      api <- domain: Return itself
    deactivate domain
    user <- api: Returns 200 OK: The word is updated
  deactivate api
deactivate user
```