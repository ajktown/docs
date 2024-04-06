# Action Group


<!-- TOC -->

- [Action Group](#action-group)
  - [Overview](#overview)
  - [Action Group Level](#action-group-level)
  - [Activity Diagram for Level Decision](#activity-diagram-for-level-decision)

<!-- /TOC -->

## Overview

`Action Group` contains a list of Actions. The main goal is to inject an appropriate level for each action once it is returned to requesters.


## Action Group Level

Action Group determines the level dynamically based on the following attributes:
- `Action`'s `createdAt`
- `Action`'s `isPerformed` (not yet implemented in April 2024)


## Activity Diagram for Level Decision
This is a basic activity diagram for how level is determined:
```plantuml
@startuml

title Action Group Level Decision

start
  if (Does Action Exist?) then (no)
    :Level is 0;
    stop
  else (yes)
    if (Is Action isPerformed==true) then (no)
      :Level is 1;
      stop
    else (yes)
      if (Is Action createdAt in time (or not late)?) then (no)
        :Level is 2;
        stop
      else (yes)
      endif
    endif
  endif
  :Level is 4;
stop
@enduml
```
