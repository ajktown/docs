# On Dev Token Sign In Handlers

<!-- TOC -->

- [On Dev Token Sign In Handlers](#on-dev-token-sign-in-handlers)
  - [Overview](#overview)

<!-- /TOC -->

## Overview
This is a basic activity diagram for the useDevTokenSignInHandlers.


```plantuml

@startuml

title useDevTokenSignInHandlers()

participant "End User" as user

box "FE" #Lightblue
  participant "Component" as fe
  participant "Hook: useDevSignIn" as hook
  participant "Hook: UseAuthPrep" as hook2
box
box "API" #Lightgreen
  participant "API" as api
box

activate user
  user -> fe: User clicks `Continue with Developer Token`
  activate fe
    fe -> hook: onDevSignIn()
    activate hook
      hook -> api: postAuthByDevTokenApi()
      activate api
        hook <- api: Successful authentication with a developer token
      deactivate api
      hook -> hook2: onGetAuthPrep()
      activate hook2
        hook2 -> hook2: Prepare auth data
        hook <- hook2: Returns nothing
      deactivate hook2
      hook -> hook: router.push(DEFAULT_MAIN_APP_PAGE)
      note left
        User can now see the default app page
      end note
      fe <- hook: Returns nothing
    deactivate hook
    user <- fe: Returns nothing
  deactivate fe
deactivate user
