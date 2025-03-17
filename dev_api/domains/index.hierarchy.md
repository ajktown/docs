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
switch ( DomainRoot )
case ()
  switch ( TODO:TITLE )
  case ()
    stop
  case ()
    stop
  endswitch
  :ActionGroup;
  :Action;
  stop
case ( archive )
  :Archive;
  stop
case ()
  switch ( auth )
  case ()
    :AccessTokenDomain;
    stop
  case ()
    :AuthPrepDomain;
    stop
  endswitch
case ()
  switch ( prefernce )
  case ()
    stop
  case ()
    stop
  endswitch
case ()
  switch ( ritual )
  case ()
    stop
  case ()
    stop
  endswitch
case ()
  switch ( semester )
  case ()
    stop
  case ()
    stop
  endswitch
case ()
  switch ( shared-resource )
  case ()
    stop
  case ()
    stop
  endswitch
case ()
  switch ( support )
  case ()
    stop
  case ()
    stop
  endswitch
case ()
  switch ( user )
  case ()
    stop
  case ()
    stop
  endswitch
case ()
  switch ( word )
  case ()
    stop
  case ()
    stop
  endswitch
endswitch

@enduml

```