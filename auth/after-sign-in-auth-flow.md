# Auth Flow

<!-- TOC -->

- [Auth Flow](#auth-flow)
  - [Sign in with Google](#sign-in-with-google)
  - [Authentication and Authorization for any API calls](#authentication-and-authorization-for-any-api-calls)

<!-- /TOC -->

## Sign in with Google


```plantuml

@startuml

title Continue with Google

participant "End User" as user
participant "FE" as fe
participant "API Gateway" as api
participant "API Middleware" as mdl
participant "API Controller" as ctl

activate user
  user -> fe: User does something that sends a request to API
  activate fe
    fe -> api: Sends API Request
    api -> mdl: Passes request
    activate mdl
      mdl -> mdl: Create HttpOnlyCookieDomain from Request
      mdl -> mdl: Create AccessTokenDomain from HttpOnlyCookieDomain
      break If AccessTokenDomain is failed to create
        fe <[#red]-- mdl : Returns failure response
        fe <[#red]-- fe : Redirects to sign in page
        user <[#red]-- fe: Asks to sign in again due to expired session
      end break
      mdl -> ctl
    deactivate mdl
    activate ctl
      ctl -> ctl: Does something (Simplified)
      fe <- ctl: Returns response (Simplified)
    deactivate ctl
    deactivate mdl
  user <- fe: Shows something (Simplified)
  deactivate fe
deactivate user


```

## Authentication and Authorization for any API calls

