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
switch ( RootDomain )
case ()
  switch ( RitualActionGroupGroupDomain )
    case ()
    switch ( RitualActionGroupDomain )
      case ()
        :RitualDomain;
        stop
      case ()
        :ActionGroupDomain;
        :ActionDomain;
        stop
      endswitch
  endswitch
case ()
  switch ( archive )
  case ()
    :ArchiveDomain;
    stop
  endswitch
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
  switch ( preference )
  case ()
    :PreferenceDomain;
    :PreferenceDicDomain;
    stop
  endswitch
case ()
  switch ( semester )
  case ()
    :SemesterChunkDomain;
    :SemesterDomain;
    :SemesterDetailsDomain;
    stop
  endswitch
case ()
  switch ( shared-resource )
  case ()
    :SharedResourceDomain;
    stop
  endswitch
case ()
  switch ( support )
  case ()
    :SupportDomain;
    stop
  endswitch
case ()
  switch ( user )
  case ()
    :UserDomain;
    stop
  endswitch
case ()
  switch ( word )
  case ()
    :WordChunkDomain;
    :WordDomain;
    stop
  endswitch
endswitch

@enduml

```