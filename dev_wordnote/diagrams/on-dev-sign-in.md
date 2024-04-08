# On Dev Sign In

<!-- TOC -->

- [On Dev Sign In](#on-dev-sign-in)
  - [Overview](#overview)

<!-- /TOC -->

## Overview
This is a basic sequence diagram for the useDevSignIn.


```plantuml

@startuml

title useDevSignIn()

participant "End User" as user

box "FE" #Lightblue
  participant "Component" as fe
  participant "Hook: useDevSignIn" as hook
  participant "Hook: useAuthPrep" as hook2
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
