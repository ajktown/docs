# On Put Preference Language

<!-- TOC -->

- [On Put Preference Language](#on-put-preference-language)
  - [Overview](#overview)

<!-- /TOC -->

## Overview
This is a basic activity diagram for the onPutPreferenceLanguage() function in the FE.


```plantuml

@startuml

title onPutPreferenceLanguage()

participant "End User" as user

box "FE" #Lightblue
  participant "Component" as fe
  participant "usePutPreferenceNativeLanguage()" as hook
  participant "usePutPreference()" as hook2
  participant "Recoil" as recoil
box
box "API" #Lightgreen
  participant "API" as api
box


activate user
  user -> fe: Click native language checkbox
  activate fe
    fe -> hook: onPutPreferenceNativeLanguage()
    activate hook
      hook -> recoil: getPromise(preferenceState)
      activate recoil
        hook <- recoil: return preferenceState
      deactivate recoil
      break if preferenceState is null
        fe <- hook: return undefined
        user <- fe: Shows nothing changed
      end break
      hook -> hook: update native language preference based on checked
      hook -> hook2: onUsePutPreference()
      activate hook2
        hook2 -> api: putPreferenceApi()
        activate api
          hook2 <- api: return modified preference
        deactivate api
        hook2 -> hook2: Save into `data`
        hook2 -> recoil: set(preferenceState, data)
        hook <- hook2: return undefined
      deactivate hook2
      fe <- hook: return undefined
    deactivate hook
    user <-fe: Does nothing
  deactivate fe
  note right
    Since the component is watching preferenceState,
    Once preferenceState is modified,
    The checkbox will be updated automatically
  end note
deactivate user
```
