### IBM - mas-bas - BAS Operator
* 

### Create a Project 
```bash
oc apply -f namespace.yaml
```
#### Create a secret named "database-credentials" for PostgreSQL DB

```bash
oc apply -f mas-bas-db-secrets.yaml
```

### Installation

These steps need to be carried out on each cluster once, to install the mas-bas operator along with necessary RBAC rules

```bash
kustomize build ${GITOPS_REPO}/mas-bas/base/subscription | \
  kubectl apply -f -
```
### 1) approve subscription plan  2) install instance 3) approve plan for services deployed for the BAS instance

```bash
kustomize build ${GITOPS_REPO}/mas-bas/base/instances/ | \
  kubectl apply -f -

```

### Approve the plan for dependent serivce - amq streams

### wait for 1 hour for installation



### Generate API key
```bash
kustomize build ${GITOPS_REPO}/mas-bas/base/apikey/ | \
  kubectl apply -f -

```