
# Get Words API

<!-- TOC -->

- [Get Words API](#get-words-api)
  - [Overview](#overview)
  - [Diagram](#diagram)

<!-- /TOC -->

## Overview
Sequence diagram for `AJK Town API` endpoint: `GET /api/v1/words`

## Diagram

```mermaid

sequenceDiagram
title: GET /api/v1/words

actor user as User
box Green API - AJK Town
  participant api as API
  participant domain as RitualGroupDomain
  participant ritual_domain as RitualDomain
end
box Crimson mongodb - AJK Town
  participant db as DB
end


activate user
  user ->> api: Requests `GET /api/v1/words`
  activate api
  deactivate api
deactivate user
```