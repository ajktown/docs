# Post Words

<!-- TOC -->

- [Post Words](#post-words)
  - [Overview](#overview)
  - [Diagram](#diagram)

<!-- /TOC -->


## Overview
Endpoint `POST /api/v1/words` is used to post a new word to the database. The user sends a request to the API with the word to be posted. The API then creates a new word document in the database and returns the created word document to the user.

## Diagram

```plantuml

@startuml

title POST /api/v1/words

participant "User" as user

box "API" #Lightgreen
  participant "API" as api
  participant "Language Detector" as lambda
  participant "SupportDomain" as domain
  participant "PreferenceDomain" as domain2
box
box "DB" #Crimson
  participant "DB" as db
box

activate user
  user -> api: POST /api/v1/words
  activate api
    break if request body does not include languageCode
      note right
        It is considered as the requesters want AJK Town API wants to detect the language of the word
      end note
      api -> lambda: Requests to detect the language of the word
      activate lambda
        api <- lambda: Returns the detected language code
      deactivate lambda
    end break
    api -> db: Posts a new word document
    activate db
      api <- db: Returns a newly posted word document
    deactivate db
    api -> db: Gets a support document of the requester
    activate db
      api <- db: Returns the support document
    deactivate db
    api -> domain: Requests updating the support document
    activate domain
      domain -> domain: Updates its own semesters array, if posted time is in a new semester
      domain -> domain: Updates its own newWordCount with +1
      domain -> db: Updates the support document by its own props
      activate db
        domain <- db: Returns the updated support document
      deactivate db
      api <- domain: Returns SupportDomain itself
    deactivate domain
    break if requester body has tags
      note right
        Preference Document's recentTags must be updated as the user introduces a new tag
      end note
      api -> domain2: Requests updating the preference document
      activate domain2
        domain2 -> db: Gets the preference document of the requester
        activate db
          domain2 <- db: Returns the preference document
        deactivate db
        domain2 -> domain2: Updates its own recentTags array
        domain2 -> db: Updates the support document by its own props
        activate db
          domain2 <- db: Returns the updated support document
        deactivate db
        api <- domain2: Returns PreferenceDomain itself
      deactivate domain2
    end break
    user <- api: Returns 200 OK: The action group is archived
  deactivate api
deactivate user
```
