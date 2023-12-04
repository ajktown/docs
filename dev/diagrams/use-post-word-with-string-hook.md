# On Post Word With String Hook

<!-- TOC -->

- [Use Post Word With String Hook](#use-post-word-with-string-hook)
  - [Overview](#overview)

<!-- /TOC -->

## Overview
This is a basic activity diagram for the usePostWordWithStingHook.


```plantuml

@startuml

title usePostWordWithStringHook()

box "FE" #Lightblue
  participant "Component" as fe
  participant "Hook" as hook
  participant "IsWritingMode" as useState
  participant "IsLoading" as useState2

  participant "Recoil" as recoil
box
box "API" #Lightgreen
  participant "API" as api
box

activate fe
  fe -> hook: onClickWritingModeOpen
  activate hook
    hook -> useState: setWritingMode(true)
    activate useState
      useState -> useState: Sets isLoading to true
    deactivate useState
    fe -> hook: onClickPostWord
    break if useInput data is undefined
      hook -> useState: setWritingMode(false)
      activate useState
      useState -> useState: Sets isLoading to false
    deactivate useState
    end break
    hook -> useState2: setLoading(true)
    activate useState2
      useState2 -> useState2: Sets isLoading to true
    deactivate useState2
    activate api
      hook -> api: handlePostWordApi(newWord)
    deactivate api
    hook -> useState2: setLoading(false)
    activate useState2
      useState2 -> useState2: Sets isLoading to false
    deactivate useState2
    hook -> useState: setUserInput(``)
    activate useState
      useState -> useState: if withWritingModeClosed && setWritingMode(false)
      hook <- useState: onClickPostWordWritingModeClose
      fe <- hook: onClickPostWord(true)
      hook <- useState: onClickPostWordWritingModeOpen
      fe <- hook: onClickPostWord(false)
```