Codefresh packages Argo CD as part of their [Hybrid runtime](https://codefresh.io/docs/docs/installation/gitops/hybrid-gitops-helm-installation/). This Helm chart can take generic Argo CD paramaters, because Argo CD is a sub-chart the values files just need to be modified to be under `argo-cd`. See [example values file](values.yaml).

Argo CD Helm supports creating config management plugins directly via the values file. This requires updating two sections.
1. [argo-cd -> configs -> cmp](https://github.com/argoproj/argo-helm/blob/main/charts/argo-cd/values.yaml)
1. [argo-cd -> repoServer -> extraContainers](https://github.com/argoproj/argo-helm/blob/main/charts/argo-cd/values.yaml#L2099-L2153)

The Argo CD Helm Chart generates a shared `argocd-cmp-cm` config map which contains all Argo CD CMP configurations as subpaths. It also supports an array of `extraContainers` to be added as sidecars on `argocd-repo-server`