This plugin will run `kustomize build --enable-helm`.

## Installation
Examples are provided with plain Kubernetes manifests and kustomize.

### Create a configmap with the CMP configuration

`kubectl apply -f https://raw.githubusercontent.com/todaywasawesome/argocd-cmp-plugin-examples/main/examples/kustomize-with-helm/plain-manifests/kustomize-build-with-helm.configmap.yaml`

### Modify Argo CD to add a sidecar

**Note: this example uses an image that supports a specific version of Kubernetes, verify the file matches your version.**

We do not recommend applying the example manifest directly from this repo, instead review the examples and modify your instance accordingly. 