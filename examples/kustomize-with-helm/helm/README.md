# Create Config Management Plugins with community Argo CD Helm chart

This example shows installation of the Kustomize with Helm plugin using the Argo CD Helm Chart.

Argo CD Helm supports creating config management plugins directly via the values file. This requires updating two sections.
1. [configs -> cmp](https://github.com/argoproj/argo-helm/blob/main/charts/argo-cd/values.yaml)
1. [repoServer -> extraContainers](https://github.com/argoproj/argo-helm/blob/main/charts/argo-cd/values.yaml#L2099-L2153)

The Argo CD Helm Chart generates a shared `argocd-cmp-cm` config map which contains all Argo CD CMP configurations as subpaths. It also supports an array of `extraContainers` to be added as sidecars on `argocd-repo-server`

View the [example values.yaml to show plugin installation](values.yaml).