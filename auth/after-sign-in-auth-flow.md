# Auth Flow

<!-- TOC -->

- [Auth Flow](#auth-flow)
  - [Sign in with Google](#sign-in-with-google)
  - [Authentication and Authorization for any API calls](#authentication-and-authorization-for-any-api-calls)

<!-- /TOC -->

## Sign in with Google


```plantuml

@startuml

title Authentication Flow

participant "End User" as user
participant "FE" as fe
box "API" #Lightgreen
  participant "API Gateway" as api
  participant "API Middleware" as mdl
  participant "AccessTokenDomain" as atd
  participant "API Controller" as ctl
box
activate user
  user -> fe: User does something that sends a request to API
  activate fe
    fe -> api: Sends API Request
    activate api
      api -> mdl: Passes request
    deactivate api
    activate mdl
      mdl -> atd: AccessTokenDomain.fromReq(ExpressJS Request)
      activate atd
        break If HttpOnly Cookie ASAT is not found or is already expired/corrupted etc
          mdl <[#red]-- atd : Fails to create AccessTokenDomain from ExpressJS Request
          fe <[#red]-- mdl : Returns failure response
          fe <[#red]-- fe : Redirects to sign in page
          user <[#red]-- fe: Asks to sign in again due to expired session
        end break
        mdl <- atd: Returns AccessTokenDomain (Contains UserId and Email)
      deactivate atd
      mdl -> mdl: Auth Middleware considers authenticated \n for the successful creation of AccessTokenDomain
      mdl -> ctl: Passes request to the controller
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

