# Argo CD Example with Plain Manfiests

The example `argocd-repo-server.deployment` shows a rendered manfiest with our helm-lookup sidecar added. You should not apply this manifest to your own cluster, but use it as an example of what a sidecar looks like. 

The `helm-lookup.yaml` shows a configmap with our settings for the plugin.


## Approach

By default and by design (with good reason), repo-server does not have access to clusters Argo CD manages. To do value lookups you'll need to package a kubeconfig file and create a secret that we can mount. This user account should have the minimal permissions required to do value lookups.

Step 1: Create the secret
`kubectl create secret generic cluster-creds -n argocd --from-file=config=./kubeconfig`

Step 2: Deploy helm-lookup.yaml
`kubectl apply -f helm-lookup.yaml -n argocd`
This contains the configuration for the plugin to run. The init step includes setting restrictive permissions on the kubeconfig file and this is required to not throw errors and warnings. 

Step 3: Update `argocd-repo-server` to include the additional init containers and cmp sidecar.
See example file `argocd-repo-server.deployment.yaml`