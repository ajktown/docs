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
  participant "Hook: useDevTokenSignInHandlers" as hook
  participant "Hook: UseAuthPrep" as authPrep
box
box "API" #Lightgreen
  participant "API" as api
box

activate user
  user -> fe: onClick `Continue with Developer Token`
  activate fe
    fe -> hook: useDevTokenSignInHandlers()
    activate hook
      hook -> api: postAuthByDevTokenApi()
      activate api
        hook <- api: Successful authentication with a developer token
      deactivate api
      hook -> authPrep: onGetAuthPrep()
      activate authPrep
        authPrep -> api: onGetAuthPrep
        activate api
          break if there is no auth prep
            authPrep <- api: Return null
          end break
          authPrep <- api: Return data
        deactivate api
        hook <- authPrep: Return undefined
      deactivate authPrep
      hook <- hook: router.push(DEFAULT_MAIN_APP_PAGE)
      break if an error occurs
        hook <- hook: throw new Error(`something went wrong`)
        hook <- hook: onError console.log(`onError; ContinueWithDevToken`)
        fe <- hook: Returns nothing
      end break
      fe <- hook: Returns nothing
    deactivate hook
    user <- fe: Returns nothing
  deactivate fe
deactivate user


      
        

