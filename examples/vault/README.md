# Create Config Management Plugins Modifying Argo CD Manifests
This plugin will allow you to use the [Argo CD Vault plugin](https://argocd-vault-plugin.readthedocs.io/en/stable/).

## Installation
Examples is provided for Codefresh's Helm chart

* [Codefresh Helm Chart](codefresh)

#### Basic Instructions

### Modify Argo CD to add a sidecar

**Note: this example uses an image that supports a specific version of Kubernetes, verify the file matches your version.**

We do not recommend applying the example manifest directly from this repo, instead review the examples and modify your instance accordingly.

## Application Definition

Below is an example of an application definition using the plugin

Note the plugin block on line 14 and 15

```
apiVersion: argoproj.io/v1alpha1
kind: Application
metadata:
  name: jenkins
spec:
  project: dev
  destination:
    namespace: dev
    server: https://kubernetes.default.svc
  source:
    path: ./manifests/jenkins-aws-secret/
    repoURL: https://github.com/lrochette/csdp_applications.git
    targetRevision: HEAD
    plugin:
      name: argocd-vault-plugin
  syncPolicy:
    syncOptions:
    - CreateNamespace=true
    automated:
      prune: true
      selfHeal: true
```
## Secret usage

Here is how to create a Kubernetes secret and get its value from AWS Secret Manager.

* jenkins/secrets: is the name of the secret in AWS Secret Manager
* pwd: is the name of the key in that secret

```
kind: Secret
apiVersion: v1
metadata:
  name: jenkins
  annotations:
    avp.kubernetes.io/path: jenkins/secrets
  labels:
    app.kubernetes.io/instance: aws-secret
    owner: laurent
type: Opaque
stringData:
  jk-password: <pwd>
```
