# On Create Shared Resource


<!-- TOC -->

- [On Create Shared Resource](#on-create-shared-resource)
  - [Overview](#overview)
  - [Security](#security)
  - [Data Security](#data-security)
  - [POST shared-resource](#post-shared-resource)

<!-- /TOC -->

## Overview

`Shared resource` is is a feature that you can share your own resource with others using `SharedResourceDomain`.


## Security
- To protect the resource, the API most of the time throws NotExistOrNoPermissionError error when:
  - The resource does not exist
  - The resource is not owned by the user
  - The resource is expired


## Data Security
- When end user posts SharedResource, it makes sure the following:
  - The shared resource does not exist
    - If already exists, it simply returns `SharedResourceDomain.fromMdb().toSharedRes()`
  - The sharing resource actually exists
  - The sharing resource is actually owned by the requester


## POST shared-resource

```plantuml

@startuml

title POST onClickShareResource()

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
      api -> domain: Requests SharedResourceDomain
      activate domain
        domain -> db: Requests sharing resource doc
        activate db
          domain <- db: Returns sharing resource od
        deactivate db
        domain -> domain: Checks if the resource is actually owned by the user.
        break if the resource is not owned by the user
          api <- domain: Throws an error NotExistOrNoPermissionError
          fe <- api: Returns 400
          user <- fe: Tells the user that it is a bad request
          note right
            By default FE should never allow the situation
            that shows the error message to the end user.
          end note
        end break
        domain -> db: Checks if the same shared-resource domain exists. Always try to get the latest one
        activate db
          domain <- db: Returns stored data
        deactivate db
        break if doc exists
          api <- domain: Returns SharedResourceDomain with the existing doc
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

