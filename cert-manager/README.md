### Cert-Manager Installation
* cert-manager is a Kubernetes add-on to automate the management and issuance of TLS certificates from various issuing sources.

### Steps to Install Cert-Manager

[Installing the Cert-Manager Operator using Openshift](https://cert-manager.io/v0.15-docs/installation/openshift/#installing-with-cert-manager-operator)

### Installation

These steps need to be carried out on each cluster once, to install the cert-manager operator

```bash
GITOPS_REPO="${HOME}/Projects/workspace/Containers/platform-gitops"
kustomize build ${GITOPS_REPO}/cert-manager | \
  kubectl apply -f -
```
