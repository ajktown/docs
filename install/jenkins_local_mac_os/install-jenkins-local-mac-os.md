# Install Jenkins on Local Mac OS

<!-- TOC -->

- [Install Jenkins on Local Mac OS](#install-jenkins-on-local-mac-os)
  - [Overview](#overview)
    - [Sub-goal](#sub-goal)
  - [Steps](#steps)
    - [Install Jenkins for Mac OS](#install-jenkins-for-mac-os)
    - [Install Necessary Plugins](#install-necessary-plugins)
      - [File System SCM](#file-system-scm)
    - [Install Optional Plugins](#install-optional-plugins)
      - [OpenID Connect Provider (OIDC Provider)](#openid-connect-provider-oidc-provider)
    - [Create Appropriate Credentials System Domain](#create-appropriate-credentials-system-domain)
    - [Set up appropriate credentials under the correct credentials system](#set-up-appropriate-credentials-under-the-correct-credentials-system)
      - [ID Naming Rules](#id-naming-rules)

<!-- /TOC -->


## Overview
The goal of this document is to share the steps to install Jenkins on a local Mac OS machine.

### Sub-goal
The indirect/sub-goal of installing Jenkins is to build/deploy locally and push to the remote server.


## Steps

### Install Jenkins for Mac OS
https://www.jenkins.io/doc/book/installing/macos/




### Install Necessary Plugins
Install the following plugins to Jenkins.

#### File System SCM
You can run Jenkins jobs from Jenkinsfile on your local device, instead of GitHub.

![install_plugin_file_system_scm](./assets/install_plugin_file_system_scm.png)


### Install Optional Plugins
#### OpenID Connect Provider (OIDC Provider)
https://plugins.jenkins.io/oidc-provider/


### Create Appropriate Credentials System Domain
Creating a separate credentials system domain for Jenkins is a good practice for least privilege access:
![credentials_system_domain](./assets/credentials_system_domain.png)


### Set up appropriate credentials under the correct credentials system

#### ID Naming Rules

`<product_name>_<local_or_cloud>_<name>_<type>`

