# On Sign Out App

<!-- TOC -->

- [On Sign Out App Hook](#on-sign-out-app-hook)
  - [Overview](#overview)

<!-- /TOC -->

## Overview
This is a basic activity diagram for the onSignOutApp() of useOnSignOutAppHook.


```plantuml

@startuml

title onSignOutApp()

participant "End User" as user

box "FE" #Lightblue
  participant "Component" as fe
  participant "Hook: onSignOutApp" as hook
  participant "Recoil" as recoil
box
box "API" #Lightgreen
  participant "API" as api
box

activate user
  user -> fe: SignOutApp
  activate fe
    fe -> hook: onSignOutAppHook
    activate hook
      hook -> api: postSignOut
      activate api
        hook <- api: Sign-out successful
      deactivate api
      hook -> recoil: Resets wordIdsState
      activate recoil
        hook -> recoil: Resets preferenceState
        recoil -> recoil: Resets Recoil states
        hook <- recoil: Return nothing
      deactivate recoil
      fe <- hook: Redirects to Welcome page
    deactivate hook
    user <- fe: Shows Welcome page
  deactivate fe
deactivate user
    