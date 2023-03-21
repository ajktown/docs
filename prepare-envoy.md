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

# Grab sample envoy config file (That the Envoy officially provides)
curl -o ~/envoy-demo-config.yaml https://www.envoyproxy.io/docs/envoy/latest/_downloads/92dcb9714fb6bc288d042029b34c0de4/envoy-demo.yaml

# Run
envoy -c ~/envoy-demo-config.yaml

# Delete the config yaml you just created
rm ~/.envoy-demo-config.yaml
```


## How to kill envoy running background 

```sh
# Where port is 10000

lsof -i tcp:10000

kill -9 <PID>

```