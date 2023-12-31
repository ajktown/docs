# On App Booting Hook

<!-- TOC -->

- [Use Is App Booted Hook](#use-is-app-booted-hook)
  - [Overview](#overview)

<!-- /TOC -->

## Overview
This is a basic activity diagram for the useIsAppBootedHook.


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
      hook -> hook: handleSignOutApp()
      hook -> hook: router.push(DEFAULT_MAIN_APP_PAGE)
      fe <- hook: Returns nothing
    deactivate hook
    user <- fe: Returns nothing
  deactivate fe
deactivate user

