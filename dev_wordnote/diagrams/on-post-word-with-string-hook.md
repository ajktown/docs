# On Post Word With String Hook

<!-- TOC -->

- [On Post Word With String Hook](#on-post-word-with-string-hook)
  - [Overview](#overview)

<!-- /TOC -->

## Overview
This is a basic sequence diagram for the usePostWordWithStingHook.


```plantuml

@startuml

title usePostWordWithStringHook()

participant "End User" as user

box "FE" #Lightblue
  participant "Component" as fe
  participant "Hook: usePostWordWithString" as hook
  participant "Lambda" as lambda
  participant "Hook: usePostWord" as hook2
  participant "Recoil" as recoil
box
box "API" #Lightgreen
  participant "API" as api
  participant "WordDomain" as domain
  participant "PreferenceDomain" as pd
box
database "MongoDB" as db

activate user
  user -> fe: User enters some words
  activate fe
    user <- fe: Shows the entered words
  deactivate fe
  user -> fe: Enters the word to posted
  activate fe
    fe -> hook: onClickPostWord()
    activate hook
      hook -> lambda: Ask lambda to parse the given string into object
      activate lambda
        hook <- lambda: Returns the perse object
      deactivate lambda
      hook -> hook2: Ask usePostWord to post the word
      activate hook2
        hook2 -> api: postWordApi()
        activate api
          api -> domain:Requests WordDomain
          activate domain
            domain -> db: Requests new word doc
            activate db
            break if tags are found, modify tags
              domain -> pd: updateWithNewTags()
              activate pd
                pd -> db: Requests to update preference data
                pd<- db:  Returns stored data
                api <- pd: Returns PreferenceDomain
              deactivate pd
            end break
            domain <- db: Returns the posted word
            deactivate db
            api <- domain: Returns the posted word
          hook2 <- api: Returns the posted word
        deactivate api
        hook2 -> recoil: set(wordIdsState,[postedWord.id,...wordIds])
        hook2 -> recoil: set(wordsFamily(postedWord.id),postedWord)
        hook2 -> recoil: set(semestersState,semesters.semesters)
        hook <- hook2: Returns nothing
      deactivate hook2
      fe <- hook: Returns nothing
    deactivate hook
    user <- fe: Returns nothing
  deactivate fe
deactivate user
```
