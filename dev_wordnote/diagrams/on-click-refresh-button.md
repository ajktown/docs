# On Click Refresh Button

<!-- TOC -->

- [On Click Refresh Button](#on-click-refresh-button)
  - [Overview](#overview)
    - [useWordsWithSemesters.hook](#usewordswithsemestershook)
    - [usePreference.hook](#usepreferencehook)

<!-- /TOC -->

## Overview
This is a basic sequence diagram for the onClickRefresh() function in the FE.

In the onClickRefresh() function, the following hooks are processed simultaneously.
　
 - use-words-with-semesters.hook

 - use-preference.hook

### useWordsWithSemesters.hook

```plantuml

@startuml

title useWordsWithSemesters()

box "FE" #Lightblue
  participant "Component" as fe
  participant "Hook" as hook
  participant "Recoil" as recoil
box
box "API" #Lightgreen
  participant "API" as api
box

  activate fe
  fe -> hook: onGetSemesters()
    activate hook
      hook -> api: getSemestersApi()
      activate api
        hook <- api: return semesters
      deactivate api
      hook -> recoil: set(semesterState, semesters)
      fe <- hook: return semesters
    deactivate hook
  break if latestSemester is undefined
  end break
    fe -> hook: onGetWords()
    activate hook
      hook -> api: getWordsApi()
      activate api
        hook <- api: return words
      deactivate api
      hook -> recoil: set(wordsFamily(word.id), word)
      hook -> recoil: set(wordIdsState, apiResponse.wordIds)
      fe <- hook: Returns nothing
    deactivate hook
```
### usePreference.hook

```plantuml

@startuml

title usePreference()

box "FE" #Lightblue
  participant "Component" as fe
  participant "Hook" as hook
  participant "Recoil" as recoil
box
box "API" #Lightgreen
  participant "API" as api
box



  activate fe
    fe -> hook: onGetPreference()
    activate hook
      hook -> api: getPreferenceApi()
      activate api
        hook <- api: return preference
      deactivate api
      hook -> recoil: set(preferenceState, data)
      fe <- hook: Returns nothing
    deactivate hook
  deactivate fe
```
