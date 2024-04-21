# Update preference's recentTags

<!-- TOC -->

- [Update preference's recentTags](#update-preferences-recenttags)
  - [Overview](#overview)
    - [recentTags in POST word](#recenttags-in-post-word)
    - [recentTags in PUT word](#recenttags-in-put-word)

<!-- /TOC -->

## Overview
This is a basic sequence diagram for that API update preference's recentTags.

API wants to store user's recent tags when the following happens:

 - new tags are posted for newly-created words (in POST word)

 - new tags are posted for already-created words　(in PUT word)


### recentTags in POST word

```plantuml

@startuml

title recentTags in POST word

box
  participant "Component" as fe
  participant "API" as api
  participant "WordModel" as wordModel
  participant "PreferenceModel" as pm
  participant "PreferenceDomain" as pd
box

activate fe
  fe -> api: POST request with word and tags
  activate api
    api -> wordModel: save(new word)
    activate wordModel
      api <- wordModel: confirm save
    deactivate wordModel
    api -> pm: get user preference
    activate pm
      api <- pm: return preference
      api -> pd: updateWithNewTags
      activate pd
        pd -> pm: save update preference
      deactivate pd
      api <- pm: confirm save
    deactivate pm
    fe <- api: return (success ot error)
  deactivate api
deactivate fe
 


```
### recentTags in PUT word

```plantuml

@startuml

title recentTags in PUT word

box
  participant "Component" as fe
  participant "API" as api
  participant "WordModel" as wordModel
  participant "PreferenceModel" as pm
  participant "PreferenceDomain" as pd
box

activate fe
  fe -> api: PUT request with word update data
  activate api
    api -> wordModel: findByIdAndUpdate(word id, update data)
    activate wordModel
      api <- wordModel: return updated word
      deactivate wordModel
      api -> api: compare tags, find new tags
      api -> pm: get user preference     
      api -> pm: get user preferences by AccessTokenDomain
      activate pm
        api <- pm: return preference
        api -> pd: updateWithNewTags
        activate pd
          pd -> pm: save update preference
        deactivate pd
        api <- pm: confirm save
      deactivate pm
      fe <- api: return updated word(WordDomain.fromMdb(updateWord))
    deactivate api
deactivate fe
```
