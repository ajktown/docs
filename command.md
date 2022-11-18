



1. Configure your AWS Setting
```shell
aws configure
# You will be then asked your access key and secret key
```

1. Log in into the ecr with the target repository
```shell
aws ecr get-login-password \
    --region <region_name> \
    | docker login --username AWS --password-stdin \
    <account_name>.dkr.ecr.<region_name>.amazonaws.com/<repository_name>
```

1. Tag you image
```shell
docker tag <your_docker_name>:latest <account_name>.dkr.ecr.us-east-2.amazonaws.com/<repository_name>
```

1. Finally push
```shell
docker push <account_name>.dkr.ecr.us-east-2.amazonaws.com/<repository_name>
```