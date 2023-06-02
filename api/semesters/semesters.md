# Semesters

<!-- TOC -->

- [Semesters](#semesters)
  - [Overview](#overview)
  - [Semesters Data are modified under the following conditions](#semesters-data-are-modified-under-the-following-conditions)
    - [Word Post X Semester Update](#word-post-x-semester-update)
    - [Word Gets returns empty string array](#word-gets-returns-empty-string-array)
  - [Semesters Data are NOT modified under the following condition](#semesters-data-are-not-modified-under-the-following-condition)
    - [Word sem is modified (word sem cannot be modified)](#word-sem-is-modified-word-sem-cannot-be-modified)

<!-- /TOC -->

## Overview

`Semesters` is like a group for a chunk of words in three months.

## Semesters Data are modified under the following conditions

Deleting a word won't immediately delete the semester, even if semester no longer has any word data.

### Word Post X Semester Update

When word is newly posted, it gets semester and simply add the semester without duplicate.

Then it will update the semester along with addedWordCount.

```plantuml

@startuml

title Word Post X Semester Update

participant "End User" as user
participant "FE" as fe
participant "API" as api
database "MongoDB" as db

activate user
  user -> fe: User add a new word
  activate fe
    fe -> api: Sends request to post a word
    activate api
      api -> db: Find Support
      activate db
        api <- db: Return Support
      deactivate db
      api -> api: Create SupportDomain
      note right
        Even if there is no SupportDomain data in db,
        it will simply create a default SupportDomain
        that will be eventually saved in db.
      end note
      api -> db: Post a word
      activate db
        api <- db: Returns response
      deactivate db
      api -> api: Update SupportDomain
      note right
        Modifies the following attributes
          - addedWordCount
          - semesters (That are always unique, but not sorted)
            - It will be sorted when it is returned to FE
      end note
      api -> db: Update Support Request
      activate db
        api <- db: Returns response
      deactivate db
      fe <- api: Returns Success with Posted Word & Support Domain
    deactivate api
    user <- fe: Shows newly created word and new semester, if needed
  deactivate fe
deactivate user


```


TODO: Link a plantuml diagram after standard doc path is set after release

### Word Gets returns empty string array

When end user requests for words with specific semester only for query, if the result is empty

Then the requested semester should be deleted.

TODO: Link a plantuml diagram after standard doc path is set after release

## Semesters Data are NOT modified under the following condition

### Word sem is modified (word sem cannot be modified)

You may copy (POST) and delete, instead of modifying it.

Even if it is modified, it will be ignored.
