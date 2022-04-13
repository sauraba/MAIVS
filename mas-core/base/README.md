
### Create MAS namespace

```bash
oc apply -f namespace.yaml
```


### Installation

Install Operators

```bash
GITOPS_REPO="/Users/saurabhgupta/Downloads/maivs-automation-Install-main/MAIVS/MAIVS"

kustomize build ${GITOPS_REPO}/mas-core/base/operator | \
  kubectl apply -f -
```
### Approve install plan for ibm-mas and ibm-common-services operators


#### Configure entitlement
Create a Docker secret that is named ibm-entitlement containing your entitlement key for the IBM Entitled Registry:

```bash
ER_KEY=<your-er-key>

oc -n mas-maivs-core create secret docker-registry ibm-entitlement \
  --docker-server=cp.icr.io \
  --docker-username=cp \
  --docker-password=$ER_KEY
```

### Install MAS instance (wait for 5 minutes to complete)

```bash
kustomize build ${GITOPS_REPO}/mas-core/base/suite | \
  kubectl apply -f -

```
