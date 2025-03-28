# Domain hierarchy

<!-- TOC -->

- [Domain hierarchy](#domain-hierarchy)
  - [Overview](#overview)

<!-- /TOC -->

## Overview

Domain `SwingGroupDomain` contains fine-grained result of every shot (or group of shots). DB stores SwingGroupDomain as `swing-groups` table. But we do not store individual swing because it is too fine-grained. Instead, we store a group of swings as a `swing-group`. This domain is responsible for managing `swing-group` data.


