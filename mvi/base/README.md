### IBM - mas-bas - BAS Operator
* 

### Create a Project 
```bash
oc apply -f ${GITOPS_REPO}/mvi/base/namespace.yaml

ER_KEY=<your-er-key>

oc -n mas-maivs-visualinspection create secret docker-registry ibm-entitlement \
  --docker-server=cp.icr.io \
  --docker-username=cp \
  --docker-password=$ER_KEY
```
#### Create SecurityContextConstraints Requirements


```bash
kustomize build ${GITOPS_REPO}/mvi/base/pre-req | \
  kubectl apply -f -
```

### Installation

These steps need to be carried out on each cluster once, to install MVI operator

```bash
kustomize build ${GITOPS_REPO}/mvi/base/operator | \
  kubectl apply -f -
```
### approve subscription plan ; create PVC (mavis-data-pvc) and copy data to PVC;  deploy instance with GPU nodes and NVIDIA operators already in place

```bash
kustomize build ${GITOPS_REPO}/mvi/base/instance/ | \
  kubectl apply -f -

```
### wait for 15 minutes for installation
