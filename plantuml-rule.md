# PlantUML Rules

<!-- TOC -->

- [PlantUML Rules](#plantuml-rules)
  - [Overview](#overview)
  - [Title Rules](#title-rules)
    - [Require Title](#require-title)
    - [Title must match to the markdown](#title-must-match-to-the-markdown)
  - [Participant Rules](#participant-rules)
    - [The order is always EndUser, FE, API, BE, DB, 3rd Party](#the-order-is-always-enduser-fe-api-be-db-3rd-party)
    - [Participant must be omitted, if not used.](#participant-must-be-omitted-if-not-used)
    - [The title of participant can be vary, but without special reasons, it should follow the standard name](#the-title-of-participant-can-be-vary-but-without-special-reasons-it-should-follow-the-standard-name)
    - [Shortened code is recommended to be 2 or 3 characters](#shortened-code-is-recommended-to-be-2-or-3-characters)
    - [Shortened code of participants must be the same](#shortened-code-of-participants-must-be-the-same)
    - [Use box, only when there are multiple participant of the same](#use-box-only-when-there-are-multiple-participant-of-the-same)

<!-- /TOC -->

## Overview

List of PlantUML rules


## Title Rules

### Require Title

Title must be given for every PlantUML diagram


### Title must match to the markdown

The markdown title and the diagram title must match

## Participant Rules

### The order is always EndUser, FE, API, BE, DB, 3rd Party

### Participant must be omitted, if not used.


### The title of participant can be vary, but without special reasons, it should follow the standard name

### Shortened code is recommended to be 2 or 3 characters

This is to make the diagram much faster/easier to read.

### Shortened code of participants must be the same

| Name     | Shortened Code | Remarks                         |
|:---------|:---------------|:--------------------------------|
| End User | user           | End User using the AJK Town App |
| FE       | fe             | Next JS Server                  |
| API      | api            | Nest JS Server                  |
| BE       | be             | N/A at this point of May 2023   |
| DB       | db (or mdb)    | MongoDB                         |


### Use box, only when there are multiple participant of the same

| Name     | Color           |
|:---------|:----------------|
| End User | Not Decided Yet |
| FE       | Lightblue       |
| API      | Lightgreen      |
| BE       | Not Decided Yet |
| DB       | Not Decided Yet |

```plantuml
participant "FE" as fe
box "API" #Lightgreen
  participant "API Gateway" as api
  participant "API Middleware" as mdl
box
```


TODO: More rules must be added