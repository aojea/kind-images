# KIND

1. Install KIND

https://kind.sigs.k8s.io/docs/user/quick-start/#installation

```
curl -Lo ./kind https://kind.sigs.k8s.io/dl/v0.15.0/kind-linux-amd64
chmod +x ./kind
```
`
2. Create a Kubernetes cluster

The Kubernetes version depends on the node image chosen, the list with the supported
Kubernetes versions and its associated image is published with the release notes:

https://github.com/kubernetes-sigs/kind/releases

```
./kind create cluster --image kindest/node:v1.25.0
```

3. Run conformance tests

We use the e2e.test binary published by the Kubernetes project directly, build
directly from the sources of the e2e framework., Suonoboy is just a consumer of this sources.

```
curl -L https://dl.k8s.io/v1.25.0/kubernetes-test-linux-amd64.tar.gz -o ./kubernetes-test-linux-amd64.tar.gz
tar xvzf ./kubernetes-test-linux-amd64.tar.gz \
--strip-components=3 kubernetes/test/bin/ginkgo kubernetes/test/bin/e2e.test
```

Run the binary indicating the report directory:

```
# export kubeconfig
./kind export kubeconfig --kubeconfig $PWD/kconfig --internal
# create folder to store the results
mkdir -p /tmp/results
# run tests
    ./e2e.test -ginkgo.v \
    --ginkgo.timeout="24h" \
    --ginkgo.focus="\[Conformance\]"" \
    --provider=skeleton \
    --kubeconfig=$PWD/kconfig \
    --report-dir=/tmp/results \
    --report-prefix=kind
```