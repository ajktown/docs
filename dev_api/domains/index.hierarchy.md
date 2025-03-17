# Domain hierarchy

<!-- TOC -->

- [Domain hierarchy](#domain-hierarchy)
  - [Overview](#overview)
  - [Domain hierarchy](#domain-hierarchy-1)

<!-- /TOC -->

## Overview

Domains are not created equal. Some domains manage other domains. But the problem is that every domain is handled under the same directory `/src/domains`. This document's goal is to clarify the hierarchy of domains in the API server. After seeing the hierarchy, you can understand the relationship between domains and how they are managed. Also you will see the naming convention for each domain.

## Domain hierarchy

```plantuml
@startuml

title Domain Hierarchy

start
switch (DomainRoot)
case ( action )
  :ActionGroup;
  :Action;
  stop
case ( archive )
  :Archive;
  stop
case (  )
  switch ( auth )
  case ( )
    :AccessTokenDomain;
    stop
  case ( )
    :AuthPrepDomain;
    stop
  endswitch
case ( preference )
  :Text 4;
  stop
case ( ritual )
  :Text 5;
  stop
case ( semester )
  :Text 5;
  stop
case ( shared-resource )
  :Text 5;
  stop
case ( support )
  :Text 5;
  stop
case ( user )
  :Text 5;
  stop
case ( word )
  :Text 5;
  stop
endswitch

@enduml

```