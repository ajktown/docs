# On Put Word By Id

<!-- TOC -->

- [On Put Word By Id](#on-put-word-by-id)
  - [Overview](#overview)

<!-- /TOC -->

## Overview
This is a basic sequence diagram for the usePutWordCache.


```plantuml

@startuml

title usePutWordHook()

participant "End User" as user

box "FE" #Lightblue
  participant "Component" as fe
  participant "Hook: usePutWordCacheByKeyHook" as hook
  participant "Hook: usePutWord" as hook2
  participant "Recoil" as recoil
box
box "API" #Lightgreen
  participant "API" as api
  participant "WordDomain" as domain
  participant "PreferenceDomain" as domain2
box
database "MongoDB" as db

activate user
  user -> fe: User enters some words
  activate fe
    user <- fe: Shows the entered words
  deactivate fe
  user -> fe: Enters ModifyButton to update words
  activate fe
    fe -> hook: onClick handleApplyCache
    activate hook
      hook -> hook2: Ask usePutWord to put the word
      activate hook2
        hook2 -> api: putWordByApi()
        activate api
          api -> domain: Requests WordDomain
          activate domain
            break if there is no field to update
              api <- domain: throw new BadRequestError
            end break
            domain -> db: Requests getById(id)
            activate db
              domain <- db: Returns the present word
              domain -> db: updateWithPutDto()
              domain <- db: Returns updated word
            deactivate db
            api <- domain: Returns updated word
          deactivate domain
          break if word has tags
            api -> domain2: Requests PreferenceDomain
            activate domain2
              domain2 -> db: Request preference doc
              activate db
                domain2 <- db: Return preference doc
              deactivate db
              api <- domain2: Returns itself (PreferenceDomain)
            deactivate domain2
            api -> domain2: preferenceDomain.updateWithNewTags()
            activate domain2
              domain2 -> db: Modifies preference doc
              activate db
                domain2 <- db: Returns the modified preference doc
              deactivate db
              api <- domain2: Returns itself (PreferenceDomain)
            deactivate domain2
          end break
          hook2 <- api: Returns the posted word
        deactivate api
        hook2 -> recoil: set(wordsFamily(wordId), modifiedWord)
      deactivate hook2
      hook <- hook2: Returns nothing
    deactivate hook
    fe <- hook: Returns nothing
  deactivate fe
  user <- fe: Returns nothing
deactivate user
              
            
