### Install Argo CD into the Kind cluster using the official installation manifests.

### Create a dedicated namespace for Argo CD:   
`kubectl create namespace argocd`

Apply the Argo CD installation manifests from the official repository. The standard installation provides full features, including the API server and UI.
`kubectl apply -n argocd -f https://raw.githubusercontent.com/argoproj/argo-cd/stable/manifests/install.yaml`

### IF you face issue, saying :
`The CustomResourceDefinition "applicationsets.argoproj.io" is invalid: metadata.annotations: Too long: may not be more than 262144 bytes`

### Apply the above command with flags `--server-side --force-conflicts` .
`kubectl apply -n argocd --server-side --force-conflicts -f https://raw.githubusercontent.com/argoproj/argo-cd/stable/manifests/install.yaml`

### Wait for the pods to be in a `Running` state:

`kubectl get pods -n argocd -w`

### Retrieve the initial admin password (username is admin):
`kubectl get secret -n argocd argocd-initial-admin-secret -o jsonpath="{.data.password}" | base64 -d
echo`

### Access the Argo CD UI 
`kubectl port-forward svc/argocd-server -n argocd 8080:443`

Deploy Sample Kubernetes Manifest (e.g., kube-argo-learnning/guestbook/guestbook-ui-deployment.yaml) 


