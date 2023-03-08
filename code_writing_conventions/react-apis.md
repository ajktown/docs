# React APIs Writing Convention


## Overview


## Rules
1. Returning API data is the de facto standard and FE will never be the standard.
1. Api functions main job is limited to the following 3 rules 
  - Receive data, without error handling.
  - May modify the returning data, but with applications to the all apis
    - Currently modifies the returning data type as following
    - ```type CustomizedAxiosResponse<T> = [T, AxiosResponse<T>]```



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