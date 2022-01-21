# SyncedSecret operator 

A Kubernetes operator to sync secrets between namespaces

The operator will read the secret from a defined source and ensure the secret is synced to defined targets. Which can be one or more namespaces.

# Build

This operator is build using the [operator-sdk framework](https://sdk.operatorframework.io/)

For more information about the operator-sdk, see the [docs](https://sdk.operatorframework.io/docs/) 

This project includes a `Makefile` to run common tasks.  

To build the docker image and push the operator image to docker registry, use: 

```sh
make docker-build docker-push IMG=mwillemsma/synced-secret-operator:0.0.2
```

# Usage


# Deploy the synced-secret-operator

Deploy the operator to your cluster. 

Check and verify [bundle/manifests](bundle/manifests) for a collection of manifests which you can apply to your cluster.


```sh
kubectl apply -f bundle/manifests
```


To sync a secret from `authorative-namespace/docker` to namespaces [a,b,c] deploy a custom resource `SyncedSecret`, see example manifest below:


secret_v1alpha1_syncedsecret_docker.yaml:
```yml
---
apiVersion: secret.willemsma.it/v1alpha1
kind: SyncedSecret
metadata:
  name: syncedsecret-docker
spec:
  source: authorative-namespace/docker
  targets:
    - a/synced-from-authorative-namespace-docker
    - b/synced-from-authorative-namespace-docker
    - c/synced-from-authorative-namespace-docker

```

To apply the manifest and let the operator manage this secret, run: 

```sh 
kubectl apply -f config/samples/secret_v1alpha1_syncedsecret_docker.yaml
```


See [config/samples/](config/samples/) for other examples.


# Testing 

Testing the operator can be done using minikube or any other development cluster.

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

If you want to see this operator in action, click the image and watch the demo below (youtube video)

[![IMAGE ALT TEXT HERE](https://img.youtube.com/vi/gNGwf81R7Sg/0.jpg)](https://youtu.be/gNGwf81R7Sg)


# Build a new bundled version of the operator (OLM) 

Create a new version of the bundle.

```sh
operator-sdk generate bundle --input-dir config --version 0.0.2
```