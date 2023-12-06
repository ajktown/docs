# Shared Resource Link

<!-- TOC -->

- [Shared Resource Link](#shared-resource-link)
  - [Overview](#overview)
  - [Shared Resource Link](#shared-resource-link-1)

<!-- /TOC -->

## Overview
Explains how shared resource link works with ajkapi server.

- Post Shared resource details [here](./on-click-share-resource.md)

## Shared Resource Link
At present, the shared resource can be attainable by anyone including non-signed in users.

```plantuml

@startuml

title Use Shared Resource Link

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
            break if the resource is expired or does not exist
              api <- domain: Throws NotExistOrNoPermissionError
              fe <- api: Throws NotExistOrNoPermissionError
              user <- fe : Shows the resource is expired, not exist or no permission
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
