# Add new field

<!-- TOC -->

- [Add new field](#add-new-field)
  - [Overview](#overview)
    - [Create Schema](#create-schema)
    - [Create Interface under domains directory](#create-interface-under-domains-directory)
    - [Create Domain](#create-domain)
    - [Modify DTO](#modify-dto)
      - [POST](#post)
      - [GET](#get)
      - [PUT](#put)
    - [Modify Word Domain](#modify-word-domain)
      - [Modify Default if required](#modify-default-if-required)
    - [Modify Factory](#modify-factory)

<!-- /TOC -->

## Overview
When you create a new schema field, you need to modify the following files.

### Create Schema

Simply copy from others and change the name only!
If you cannot come up with a name, you can ask ChatGPT for help.

### Create Interface under domains directory
Before create domain, create the interface for the domain.

### Create Domain


### Modify DTO

Delete does not exist as many times delete only requires deleting id.
The permission is checked by the requester identity attached on http headers.

#### POST

#### GET

#### PUT

### Modify Word Domain

#### Modify Default if required


### Modify Factory

