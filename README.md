# kind-images

This repository contains a CircleCI job that uses kind master version
to create node images with kubernetes master version.

These images are published every night with the format:

aojea/kindnode:kind<kind_commit>k8s<kubernetes_commit>

## Important

These node images are created with master version of kind, is it possible
that have incompatibilities with previous stable releases.
