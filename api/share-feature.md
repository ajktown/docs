# Share Feature


<!-- TOC -->

- [Share Feature](#share-feature)
  - [Overview](#overview)
  - [POST shared-resource](#post-shared-resource)
  - [GET shared-resource](#get-shared-resource)

<!-- /TOC -->

## Overview

Share feature is basically share your word card with others by generating SharedResourceDomain.


## POST shared-resource

```plantuml

@startuml

title POST shared-resource

participant "End User" as user
participant "FE" as fe
box "API" #Lightgreen
  participant "API" as api
  participant "SharedResourceDomain" as domain
box
database "MongoDB" as db

activate user
  user -> fe: User clicks the share button
  activate fe
    fe -> fe: Opens A dialog with loading indicator
    fe -> api: Sends API Request POST /api/v1/shared-resource
    activate api
      break if dto does not contain which resource the requester is asking for
        fe <- api: throw BadRequestError 400 error
        note left
          Note that as DTO requires only one of the resource id, it cannot be
          automatically detected.
        end note
        user <- fe: Tells the user that it is a bad request
        note right
          By default FE should never allow the situation
          that shows the error message to the end user.
        end note
      end break
      api -> domain: Requests SharedResourceDomain to be created
      activate domain
        domain -> db: Requests resource information
        activate db
          domain <- db: Returns resource information
        deactivate db
        domain -> domain: Checks if the resource is actually owned by the user.
        break if the resource is not owned by the user
          api <- domain: Returns 400
          note right
            It simply throws an error NotExistOrNoPermissionError
              - NotExistOrNoPermissionError:
                - Either the resource does not exist
                - Or the resource is not owned by the user
          end note
          fe <- api: Returns 400
          user <- fe: Tells the user that it is a bad request
          note right
            By default FE should never allow the situation
            that shows the error message to the end user.
          end note
        end break
        domain -> db: Checks if the same shared-resource domain exists
        activate db
          domain <- db: Returns stored data
        deactivate db
        break if more than two exists, it deletes the old ones and leave the latest one
          domain -> db: Deletes the old ones
          activate db
            domain <- db: Returns the result
          deactivate db
        end break
        domain -> db: Creates a new shared-resource domain.post()
        activate db
          domain <- db: Returns the result
        deactivate db
        api <- domain: Returns SharedResourceDomain
      deactivate domain
      fe <- api: SharedResourceDomain.toResDTO()
    deactivate api
  fe -> fe: Copies the generated URL to clipboard of the end user.
  fe -> fe: The loading indicator disappears
  user <- fe: Tells the user that the URL is copied to clipboard
  deactivate fe
  user -> user: User has the link that can be shared with others
deactivate user


```

## GET shared-resource
At present, the shared resource can be attainable by anyone including non-signed in users.

```plantuml

@startuml

title GET shared-resource

participant "End User" as user
participant "FE" as fe
box "API" #Lightgreen
  participant "API" as api
  participant "SharedResourceDomain" as domain
box
database "MongoDB" as db

activate user
  user -> fe: User opens a shared link
  activate fe
    fe -> fe: Opens A dialog with loading indicator
    fe -> api: Sends API Request GET /api/v1/shared-resource
    activate api
      api -> domain: Requests SharedResourceDomain to be created
      activate domain
        domain -> db: Requests shared resource doc
        activate db
          domain <- db: Returns resource doc
        deactivate db
        api <- domain: Returns SharedResourceDomain
        deactivate domain
        api -> domain: Requests SharedResourceDomain.toResDTO()
          activate domain
            break if the resource is expired
              api <- domain: Returns SharedResourceDomain.toResDTO()
              fe <- api: Returns the response DTO
              note left
                The expired shared resource won't contain
                any resource information.
              end note
              user <- fe : Shows the message that the resource is expired
            end break
            domain -> db: Requests resource information
            activate db
              domain <- db: Returns resource information
            deactivate db
            api <- domain: Returns SharedResourceDomain.toResDTO()
          deactivate domain
        fe <- api: Returns the response DTO
    deactivate api
  fe -> fe: The loading indicator disappears
  user <- fe: Shows the shared resource
  user <- fe: Shows the post word button, if the user is signed in
  deactivate fe
  user -> user: User has the link shared resourced from others (or oneself)
deactivate user


```