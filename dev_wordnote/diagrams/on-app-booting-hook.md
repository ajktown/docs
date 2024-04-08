# On App Booting Hook

<!-- TOC -->

- [On App Booting Hook](#on-app-booting-hook)
  - [Overview](#overview)

<!-- /TOC -->

## Overview
This is a basic sequence diagram for the useIsAppBootedHook.


```plantuml

@startuml

title useIsAppBootedHook()

participant "End User" as user

box "FE" #Lightblue
  participant "Component" as fe
  participant "Hook: useIsAppBooted" as hook
box

activate user
  user -> fe: open app
  activate fe
    fe -> hook: useIsAppBooted
    activate hook
      break if there is no authPrep or the user is not signed in
        hook -> hook: handleSignOutApp()
        fe <- hook: Returns nothing
      end break
      hook -> hook: router.push(DEFAULT_MAIN_APP_PAGE)
      fe <- hook: Returns nothing
    deactivate hook
    user <- fe: Returns nothing
  deactivate fe
deactivate user

