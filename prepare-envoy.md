# Prepare Envoy

<!-- TOC -->

- [Prepare Envoy](#prepare-envoy)
  - [Overview](#overview)
  - [Steps](#steps)
  - [How to kill envoy running background](#how-to-kill-envoy-running-background)

<!-- /TOC -->

## Overview

Envoy is L7 proxy and communication bus designed for large modern service oriented architectures.


## Steps

```sh

# install envoy
brew update && brew install envoy


```

## How to kill envoy running background 

```sh
# Where port is 10000

lsof -i tcp:10000

kill -9 <PID>

```