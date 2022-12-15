# React APIs Writing Convention


## Overview


## Rules
1. Returning API data is the de facto standard and FE will never be the standard.
1. Returned data of API 


## DDD

  | Source        | Prefix          | Example            |
  |:--------------|:----------------|:-------------------|
  | API Server    | ~Domain         | WordDataDomain     |
  | FE            | ~Data           | WordData           |
  | FE Modifiable | ~DataModifiable | WordDataModifiable |

## DTOs

  | Source         | Prefix                       | Example            |
  |:---------------|:-----------------------------|:-------------------|
  | API Server DTO | Controller Name + RequestDTO | PutWordRequestDTO  |
  | FE Modifiable  | ~DataModifiable              | WordDataModifiable |