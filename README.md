# kind-images

## Kind and Kubernetes nightlies

This repository contains a job that uses kind master version
to create node images with kubernetes master version.

These images are published every night with the format:

```
aojea/kindnode:kind<kind_commit>k8s<kubernetes_commit>
```

### Important

These node images are created with master version of kind, is it possible
that have incompatibilities with previous stable releases.

### CRIO images

There are images published with CRIO and latest stable Kind versions, the Kubernetes version used is the latest stable published by Kind.

You can find the images with the following format quay.io/aojea/kindnode:crio$(timestamp) in:
https://quay.io/repository/aojea/kindnode?tab=tags

Reference: https://gist.github.com/aojea/bd1fb766302779b77b8f68fa0a81c0f2

### Usage

```
# Download kind configuration file to patch the kubelet runtime in order to use CRIO instead of containerd
wget https://raw.githubusercontent.com/aojea/kind-images/master/kind-crio.yaml
# Create the cluster with the customized Kind node image
kind create cluster --name crio --image quay.io/aojea/kindnode:crio1630331170 --config kind-crio.yaml 
```





