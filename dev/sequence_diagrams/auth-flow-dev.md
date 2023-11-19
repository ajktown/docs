# Auth Flow

<!-- TOC -->

- [Auth Flow](#auth-flow)
  - [Get ASAT without 3rd party Oauth for developers](#get-asat-without-3rd-party-oauth-for-developers)
    - [ASAT](#asat)
  - [Overview](#overview)
  - [Continue with Dev Token for developers](#continue-with-dev-token-for-developers)

<!-- /TOC -->

## Get ASAT without 3rd party Oauth for developers

### ASAT

AJK Town Secured Access Token

## Overview

- The dev token generation does not depend on the MongoDB connection
  - It is hard coded inside of the API Server

- The dev token generation does not depend on internet.
  - Does not require 3rd part Oauth


## Continue with Dev Token for developers

```plantuml

@startuml

title Continue with Dev Token for developers

participant "Developer User" as user
participant "FE" as fe
box "API" #Lightgreen
  participant "API" as api
  participant "AccessTokenDomain" as atd
box

activate user
  user -> fe: Developer opens AJK Town App
  activate fe
    fe -> fe: Runs use-is-app-booted
    fe -> api: Asks who this end user is
    activate api
      api -> api: Validates user if ASAT exists.
      api -> api: Grabs the mode of the env. (dev or prod)
      fe <- api: Returns user info and env data
    deactivate api
    user <- fe: Shows Continue with dev-token, only under non-production
    user -> fe: Clicks Continue with dev-token
    fe -> api: /auth/dev-token
    activate api
      api -> api: Checks if it is local mode
      api -> atd: AccessTokenDomain.withDevUser()
      activate atd
        break if it is production mode
          api <[#red]-- atd : Fails to create AccessTokenDomain
          fe <[#red]-- api : Returns failure response
          fe <[#red]-- fe : Redirects to sign in page
          user <[#red]-- fe: Asks to sign in in a different method
        end break
        api <- atd: Successfully creates AccessTokenDomain
      deactivate atd
      fe <- api: Attaches HttpOnly AccessTokenDomain.generateToken() to Nest JS Response
    deactivate api
    user <- fe: Shows successful sign in
  deactivate fe
  user -> user: Use application with signed in status
deactivate user


```
