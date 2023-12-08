This is a simple nginx application to demonstarte working with argocd ([readthedocs](https://argo-cd.readthedocs.io/en/stable/)).

Inspired by this [Tutorial](https://medium.com/@mehmetodabashi/installing-argocd-on-minikube-and-deploying-a-test-application-caa68ec55fbf)

Script to launch Minikube with ArgoCD:
```bash
minikube start
kubectl create ns argocd
kubectl apply -n argocd -f https://raw.githubusercontent.com/argoproj/argo-cd/stable/manifests/install.yaml
echo "waiting for argocd-server"
while [[ $(kubectl -n argocd get pods -l app.kubernetes.io/name=argocd-server -o 'jsonpath={..status.conditions[?(@.type=="Ready")].status}') != "True" ]]; do echo "waiting for argocd-server" && sleep 1; done
PASSWORD=$(kubectl -n argocd get secret argocd-initial-admin-secret -o jsonpath="{.data.password}" | base64 -d; echo -n)
echo "\nvisit http://localhost:8080"
echo "user:     admin"
echo "password: $PASSWORD\n"
kubectl port-forward svc/argocd-server -n argocd 8080:443
```

To run all examples in this project you can use this predefined yaml, after addnig this repository to Argo-CD's repositories.
```yaml
apiVersion: argoproj.io/v1alpha1
kind: Application
metadata:
  name: my-app
spec:
  destination:
    name: ''
    namespace: default
    server: 'https://kubernetes.default.svc'
  source:
    path: .
    repoURL: 'https://github.com/amalic/kubernetes-argocd'
    targetRevision: HEAD
    directory:
      recurse: true
  sources: []
  project: default
  syncPolicy:
    automated:
      prune: false
      selfHeal: false
project: default
source:
  repoURL: 'https://github.com/amalic/kubernetes-argocd'
  path: .
  targetRevision: HEAD
  directory:
    recurse: true
    jsonnet: {}
destination:
  server: 'https://kubernetes.default.svc'
  namespace: default
syncPolicy:
  automated: {}
```