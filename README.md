# SyncedSecret operator 

A Kubernetes operator to sync secrets between namespaces

# 

# Build

This operator is build using the [operator-sdk framework](https://sdk.operatorframework.io/)

For more information about the operator-sdk, see the [docs](https://sdk.operatorframework.io/docs/) 

This project includes a `Makefile` to run common tasks.  

To build the docker image and push the operator image to docker registry, use: 

```sh
make docker-build docker-push IMG=mwillemsma/synced-secret-operator:0.0.2
```

# Usage


See samples/


# Testing 

Testing the operator can be done using minikube. 

Create a cluster
```sh
minikube start -p dev --memory 3092 --cpus 2 --kubernetes-version=1.23.1
```

Run molecule to deploy the resources to k8s

```sh
OPERATOR_IMAGE=mwillemsma/synced-secrets-operator molecule converge
```

Verify the operator 


```sh
OPERATOR_IMAGE=mwillemsma/synced-secrets-operator molecule verify
```


# Demo

If you want to see this operator in action watch the demo below

[![IMAGE ALT TEXT HERE](https://img.youtube.com/vi/gNGwf81R7Sg/0.jpg)](https://youtu.be/gNGwf81R7Sg)