# Shared Resource By URL

<!-- TOC -->

- [Shared Resource By URL](#shared-resource-by-url)
  - [Overview](#overview)
  - [Shared Resource Link](#shared-resource-link)

<!-- /TOC -->

## Overview
Explains how shared resource link works with ajkapi server.

- The link contains the base64 encoded string of the resource id
  - And therefore the FE can use the ID directly.

- Post Shared resource details [here](./on-click-share-resource.md)

## Shared Resource Link
At present, the shared resource can be attainable by anyone including non-signed in users.

```plantuml

@startuml

title GET Use Shared Resource by URL

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
      api -> domain: Requests SharedResourceDomain
      activate domain
        domain -> db: Requests shared resource doc
        activate db
          domain <- db: Returns resource doc
        deactivate db
        break if the shared-resource (does not exist) || (is expired && not owned by the user)
          api <- domain: NotExistOrNoPermissionError
          note left
            If the resource is expired, it is considered as
            the owner of the resource no longer wishes to share to others
            and therefore should throw NotExistOrNoPermissionError
          end note
          fe <- api: Throws NotExistOrNoPermissionError
          user <- fe : Shows the resource is expired, not exist or no permission
        end break
        api <- domain: Returns SharedResourceDomain
        deactivate domain
        api -> domain: Requests SharedResourceDomain.toResDTO()
          activate domain
            domain -> db: Requests resource information
            activate db
              domain <- db: Returns resource information
            deactivate db
            break if the resource does not exist
              domain -> db: Delete the shared resource
              api <- domain: NotExistOrNoPermissionError
              note left
                Since the resource does not exist at all,
              end note
              fe <- api: Throws NotExistOrNoPermissionError
              user <- fe : Shows the resource is expired, not exist or no permission
              note right
                The visuals should be identical to the owners & non-owners
              end note
            end break
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
