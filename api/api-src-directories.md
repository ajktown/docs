# Api Source Directories

<!-- TOC -->

- [Api Source Directories](#api-source-directories)
  - [Overview](#overview)
  - [Each Job](#each-job)
  - [Source directory](#source-directory)
    - [Controllers](#controllers)
    - [Domains](#domains)
    - [DTO](#dto)
    - [Factories](#factories)
    - [Handlers](#handlers)
    - [Lambdas](#lambdas)
    - [Middleware](#middleware)
    - [Modules](#modules)
    - [Prompts](#prompts)
    - [responses](#responses)

<!-- /TOC -->

## Overview

Organize source directories for consistency


## Each Job

| Job         | Job                                                                          |
|:------------|:-----------------------------------------------------------------------------|
| Controllers | Return .toResDTO() & Prepare atd                                             |
| Service     | Prepares Model & Return Domain or void for response                          |
| Domain      | Defines Centralized business actions. Use given model to update db if needed |

## Source directory 

- Please organize in alphabetical order
  - i.e) Controllers, Domains, DTO, ...

### Controllers
- Exposed API to the end user.
- Should be directly telling which API it is.
- Always uses `Service` for the logic.
- Handlers error by `controller.root.ts`
- No Try Catch

### Domains
- The herb of domains
- Main domain's file name should match to the directory
  - i.e directory word = word.domain.ts (Main domain)
- Sub domains for the main domain should start with `index.sub-domain.ts`
- Sub domain of sub domain should start with `index.sub-domain.sub-sub-domain.ts`

### DTO
- Handles the random request of end user
- Never trust end user's input, even with the FE that is created by the AJK Town.
- Responsible to have default data, data validity, type so that the rest of components can use it with trust inside of the API.

### Factories
- Factories are the list of functions to convert [DTO](#dto) proven data into Database (MongoDB) query.
- Never use plain or raw data. Always use DTO as params.


### Handlers
- Non-business functions that you can use freely
- Never put business logic inside.

### Lambdas
- Business logic included function that you use for that service only (This case, API only)
- Env data should be managed inside of the lambda file.

### Middleware
- Middleware component for Controllers and Services.
- Authentication, Logging will be handled here.


### Modules
- Handles import. This is Nest JS inspired architecture.

### Prompts
- Prompts is AI generation directory AJK Town named it.
- Basically it handles ChatGPT AI texts and requests
- Pretty much the same as the `Services`, but only for AI.

### responses
- List of response data of the `services` (not controllers)
