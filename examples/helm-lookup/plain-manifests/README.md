# Argo CD Example with Plain Manfiests

The example `argocd-repo-server.deployment` shows a rendered manfiest with our helm-lookup sidecar added. You should not apply this manifest to your own cluster, but use it as an example of what a sidecar looks like. 

The `kustomize-build-with-helm.configmap.yaml` shows a configmap with our settings for the plugin.