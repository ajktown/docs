
# Secret Yaml Setup
<!-- TOC -->

- [Secret Yaml Setup](#secret-yaml-setup)
  - [Overview](#overview)
  - [Template is managed here](#template-is-managed-here)
  - [Create empty secret.yaml file](#create-empty-secretyaml-file)
    - [How to store?](#how-to-store)
    - [Sample Result](#sample-result)
    - [How to decode the encoded value](#how-to-decode-the-encoded-value)

<!-- /TOC -->

## Overview

Unlike other k8s yaml files `deployment.yaml` or `service.yaml`, `secret.yaml` must be created separately as it will contain sensitive data that should not be exposed to the public.

## Template is managed here

[Here](./05_secret.yaml) is the template for `secret.yaml` file.

Warning! Do not change the keys or `.metadata.name` of the template, as the keys are depended by the [deployment.yaml](https://github.com/ajktown/api/blob/19a3181bb1bf3206954529a314534d1099f4fea4/k8s/deployment.yaml#L20-L45) file of ajktown api.

## Create empty secret.yaml file

WARNING! Make sure that the file name is `secret.yaml`  so that it can be gitignored and not become public.

The empty secret should be stored here: https://github.com/ajktown/api/tree/main/k8s




### How to store?

Let's say, you want to put `google_client_id: this-is-your-secret-google-client-id`

If you directly put `this-is-your-secret-google-client-id`, it would not read correctly.

You need to manually base64 encode it. (Remember that base64 is not encryption and can be decoded easily by anyone else so do not think that it is safe to store in public, after you encode it)

```sh

# Always make sure to put -n, as without it, it will contain \n which then won't work as expected
echo -n  "this-is-your-secret-google-client-id" | base64
# result sample)
# dGhpcy1pcy15b3VyLXNlY3JldC1nb29nbGUtY2xpZW50LWlkCg==
```
Then, you can put the result in `secret.yaml` file.

```yaml
apiVersion: v1
kind: Secret
metadata:
  ...
type: Opaque
data:
  google_client_secret: dGhpcy1pcy15b3VyLXNlY3JldC1nb29nbGUtY2xpZW50LWlkCg==
  ...
```

Do the same for other secrets values that is listed on the template.

### Sample Result
The following data is dummy data and not real data.

```yaml
apiVersion: v1
kind: Secret
metadata:
  name: ajktown-api-secret
  namespace: ajktown
type: Opaque
data:
  # ! The following data is dummy data and not real data.
  mdb_prod_uri: VE9ETzpwdXRfeW91cl9tb25nb2RiX3VyaV9oZXJlCg==
  jwt_token_secret: VE9ETzpwdXRfeW91cl9qd3RfdG9rZW5fc2VjcmV0X2hlcmUK
  open_ai_key: VE9ETzpwdXRfeW91cl9vcGVuX2FpX2tleV9oZXJlCg==
  google_client_id: VE9ETzpwdXRfeW91cl9nb29nbGVfY2xpZW50X2lkX2hlcmUK
  google_client_secret: VE9ETzpwdXRfeW91cl9nb29nbGVfY2xpZW50X3NlY3JldF9oZXJlCg==
```

### How to decode the encoded value

You can always decode the encoded value as following

```sh

echo "VE9ETzpwdXRfeW91cl9nb29nbGVfY2xpZW50X3NlY3JldF9oZXJlCg==" | base64 --decode
# TODO:put_your_google_client_secret_here

```
