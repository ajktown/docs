# Prepare Envoy

<!-- TOC -->

- [Prepare Envoy](#prepare-envoy)
  - [Overview](#overview)
  - [Steps](#steps)
    - [Prerequisites](#prerequisites)
    - [Test routing](#test-routing)
    - [Modify scripts like the below:](#modify-scripts-like-the-below)
    - [Test](#test)
  - [Troubleshoots](#troubleshoots)

<!-- /TOC -->

## Overview

Envoy is L7 proxy and communication bus designed for large modern service oriented architectures.

We will test server mesh by doing 


## Steps

### Prerequisites

```sh

# install envoy
brew update && brew install envoy

# Grab sample envoy config file (That the Envoy officially provides)
curl -o ~/envoy-demo-config.yaml https://www.envoyproxy.io/docs/envoy/latest/_downloads/92dcb9714fb6bc288d042029b34c0de4/envoy-demo.yaml

# Run
envoy -c ~/envoy-demo-config.yaml

```

### Test routing
```sh

# Download and run echo server docker

docker run -d -p 4000:80 ealen/echo-server

```

### Modify scripts like the below:
```yaml
static_resources:
  listeners:
  - name: listener_0
    address:
      socket_address:
        protocol: TCP
        address: 127.0.0.1 # localhost
        port_value: 10000 # listening port; 80 requires sudo for envoy
    filter_chains:
    - filters:
      - name: envoy.filters.network.http_connection_manager
        typed_config:
          "@type": type.googleapis.com/envoy.extensions.filters.network.http_connection_manager.v3.HttpConnectionManager
          stat_prefix: ingress_http
          access_log:
          - name: envoy.access_loggers.stdout
            typed_config:
              "@type": type.googleapis.com/envoy.extensions.access_loggers.stream.v3.StdoutAccessLog
          http_filters:
          - name: envoy.filters.http.router
            typed_config:
              "@type": type.googleapis.com/envoy.extensions.filters.http.router.v3.Router
          route_config:
            name: local_route
            virtual_hosts:
            - name: local_service
              domains: ["*"]
              routes:
              - match:
                  prefix: "/hello-world"
                direct_response:
                  status: 200
                  body:
                    inline_string: "AJ! Hello, World!"
              - match:
                  prefix: "/echo"
                route:
                  cluster: echo-server-cluster
  clusters:
  - name: echo-server-cluster
    type: STATIC
    load_assignment:
      cluster_name: echo-server-cluster
      endpoints:
      - lb_endpoints:
        - endpoint:
            address:
              socket_address:
                address: 127.0.0.1
                port_value: 4000

```

### Test
```sh
curl localhost:10000/hello-world

# Test echo server
# Request -> Envoy (10000) -> Echo server(4000)
curl localhost:10000/echo


```

## Troubleshoots

```sh
# Where port is 10000

lsof -i tcp:10000

kill -9 <PID>

# Delete the config yaml you just created
rm ~/.envoy-demo-config.yaml

```