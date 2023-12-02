# On Click Refresh Button

<!-- TOC -->

- [On Click Refresh Button](#on-click-refresh-button)
  - [Overview](#overview)
    - [Most Detailed Ones](#most-detailed-ones)

<!-- /TOC -->

## Overview
This is a basic activity diagram for the onClickRefresh() function in the FE.

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
  Par Click refresh
  Par GetWordsWithSemesters
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
  end par
    fe -> hook: getPreference()
    activate hook
      hook -> api: getPreferenceApi()
      activate api
        hook <- api: return preference
      deactivate api
      hook -> recoil: set(preferenceState, data)
      fe <- hook: Returns nothing
  end par
    deactivate hook
  user <- fe: End Process with Loading Ends.
  deactivate fe
deactivate user
```