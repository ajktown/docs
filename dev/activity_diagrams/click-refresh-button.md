# Click Refresh Button

<!-- TOC -->

- [Click Refresh Button](#click-refresh-button)
  - [Overview](#overview)
    - [Most Detailed Ones](#most-detailed-ones)
    - [Second Most Detailed](#second-most-detailed)
    - [Simplest](#simplest)

<!-- /TOC -->

## Overview
This is a basic activity diagram for the onClickRefresh() function in the FE.

![refresh_button](./assets/refresh_button.png)

### Most Detailed Ones
![on_click_refresh_activity_diagram](./assets/on_click_refresh_activity_diagram.png)

<details><summary >plantuml code</summary>

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
</details>

### Second Most Detailed
![on_click_refresh_button_second_most_detailed](./assets/on_click_refresh_button_second_most_detailed.png)
<details><summary >plantuml code</summary>

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
</details>

### Simplest
![on_click_refresh_simplest_activity_diagram](./assets/on_click_refresh_simplest_activity_diagram.png)
<details><summary >plantuml code</summary>

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
</details>