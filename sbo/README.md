### Service Binding Operator

### Installation


```bash
kustomize build ${GITOPS_REPO}/sbo | \
  kubectl apply -f -
```
### approve the plan