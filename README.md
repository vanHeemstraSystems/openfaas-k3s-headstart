openfaas-k3s-headstart
# OpenFaaS k3s - Headstart

Based on "Installing OpenFaaS On k3s (Single Node)" at https://midnightprogrammer.net/post/installing-openfaas-on-k3s-single-node/

See also "OpenFaaS Tutorial: Build and Deploy Serverless Java Functions" at https://karthi-net.medium.com/openfaas-tutorial-build-and-deploy-serverless-java-functions-bcf4e08c3a28

If you have ever got your hands on Azure Function or on AWS Lambda, then you might be familiar with the concept of serverless computing. So in order to test the concept of a function (serverless function), we have to have an Azure or an AWS account. The SDK from both the platforms allow you to build, develop and test the functions on your local development machine, but when it comes to production environment, you again have to turn yourself to Azure or AWS for hosting it. 

[OpenFaaS](https://www.openfaas.com/) is an open-source product developed by [Alex Ellis](https://github.com/alexellis) which help developers to deploy event-driven functions, time triggered and microservices to Kubernetes without repetitive, boiler-plate coding. Let’s see how we can deploy OpenFaas on Ubuntu 20.04 LTS using k3s. You can also make use of another Kubernetes flavour which suites your needs.

## 100 - Prerequisites
See [README.md](./100/README.md)

## 200 - Installing k3s
See [README.md](./200/README.md)

## 300 - Installing faas-cli
See [README.md](./300/README.md)

## 400 - Installing arkade
See [README.md](./400/README.md)

## 500 - Installing OpenFaaS
See [README.md](./500/README.md)

## 600 - Acquire Password for OpenFaaS UI (OpenFaaS Portal)
See [README.md](./600/README.md)

## 700 - Access OpenFaaS UI (OpenFaaS Portal)
See [README.md](./700/README.md)
