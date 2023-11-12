# On Click Refresh Button

<!-- TOC -->

- [On Click Refresh Button](#on-click-refresh-button)
  - [Overview](#overview)
    - [Most Detailed Ones](#most-detailed-ones)
    - [Second Most Detailed](#second-most-detailed)
    - [Simplest](#simplest)

<!-- /TOC -->

## Overview
This is a basic activity diagram for the onClickRefresh() function in the FE.

![refresh_button](./assets/refresh_button.png)

### Most Detailed Ones

```plantuml

@startuml

title onClickRefresh()

participant "End User" as user

box "FE" #Lightblue
  participant "Component" as fe
  participant "Hook" as hook
  participant "Recoil" as recoil
box
box "API" #Lightgreen
  participant "API" as api
box


activate user
  user -> fe: Click refresh button
  activate fe
  fe -> hook: getSemesters()
    activate hook
      hook -> api: getSemestersApi()
      activate api
        hook <- api: return semesters
      deactivate api
      hook -> recoil: set(semesterState, semesters)
      fe <- hook: return semesters
    deactivate hook
  break if latestSemester is undefined
    user <- fe: End Process with Loading Ends.
  end break
    fe -> hook: getWords()
    activate hook
      hook -> api: getWordsApi()
      activate api
        hook <- api: return words
      deactivate api
      hook -> recoil: set(wordsFamily(word.id), word)
      hook -> recoil: set(wordIdsState, apiResponse.wordIds)
      fe <- hook: Returns nothing
    deactivate hook
    fe -> hook: getPreference()
    activate hook
      hook -> api: getPreferenceApi()
      activate api
        hook <- api: return preference
      deactivate api
      hook -> recoil: set(preferenceState, data)
      fe <- hook: Returns nothing
    deactivate hook
  user <- fe: End Process with Loading Ends.
  deactivate fe
deactivate user
```

### Second Most Detailed
```plantuml
@startuml

title onClickRefresh()

participant "End User" as user

box "FE" #Lightblue
  participant "FE" as fe
  participant "Hook" as hook
  participant "Recoil" as recoil
box
box "API" #Lightgreen
  participant "API" as api
box

activate user
  user -> fe: Click refresh button
  activate fe
  fe -> api: getSemesters()
    activate api
      fe <- api: return semesters
    deactivate api
  break if latestSemester is undefined
    user <- fe: Shows nothing
  end break
    fe -> api: getWords()
    activate api
      fe <- api: return words
    deactivate api
    fe -> api: getPreference()
    activate api
      fe <- api: return preference
    deactivate api
  user <- fe: Shows refreshed words
  deactivate fe
deactivate user
```


### Simplest
```plantuml

@startuml

title onClickRefresh()

participant "End User" as user

box "FE" #Lightblue
  participant "FE" as fe
box
box "API" #Lightgreen
  participant "API" as api
box

activate user
  user -> fe: Click refresh button
  activate fe
  fe -> api: getSemesters()
    activate api
      fe <- api: return semesters
    deactivate api
  break if latestSemester is undefined
    user <- fe: Shows nothing
  end break
    fe -> api: getWords()
    activate api
      fe <- api: return words
    deactivate api
    fe -> api: getPreference()
    activate api
      fe <- api: return preference
    deactivate api
  user <- fe: Shows refreshed words
  deactivate fe
deactivate user
```