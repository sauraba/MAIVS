### IBM - SLS - Licensing Service Installation
* IBM Suite License Service (SLS) is a token-based licensing system based on Rational License Key Server (RLKS) with MongoDB as the data store.

### Steps to Install IBM - SLS Suite License Service



#### Configure entitlement
Create your namespace, for example, ibm-sls and create a Docker secret that is named ibm-entitlement containing your entitlement key for the IBM Entitled Registry:


```bash
ER_KEY=<your-er-key>
eyJhbGciOiJIUzI1NiJ9.eyJpc3MiOiJJQk0gTWFya2V0cGxhY2UiLCJpYXQiOjE1OTMwOTI2MzEsImp0aSI6IjU2Yzg0YzE5YmJkZTQyOGM4OWIzMjMxZTI1MDU1MTIzIn0.iGOgy1zLwO5oWNkDqUxl2_VhMFPyP06OPajLLP1pwdY
oc apply -f namespace.yaml
oc -n ibm-sls create secret docker-registry ibm-entitlement \
  --docker-server=cp.icr.io \
  --docker-username=cp \
  --docker-password=$ER_KEY
```

#### Configure MongoDB credentials
Create a secret in the namespace where you plan to deploy SLS that contains the MongoDB credentials:
```bash
oc apply -f sls-mongo-creds-secret.yaml
```

### Set Cluster Ingress domain

```bash
oc apply -f ingress.yaml
```

### Installation

These steps need to be carried out on each cluster once, to install the cert-manager operator along with necessary RBAC rules

```bash
GITOPS_REPO="/Users/saurabhgupta/Downloads/maivs-automation-Install-main/MAIVS"
kustomize build ${GITOPS_REPO}/ibm-sls-licensing/base/catalog | \
  kubectl apply -f -

kustomize build ${GITOPS_REPO}/ibm-sls-licensing/base/operator | \
  kubectl apply -f -
```
### Approve install plan

```bash
kustomize build ${GITOPS_REPO}/ibm-sls-licensing/base/LicenseService | \
  kubectl apply -f -

```
