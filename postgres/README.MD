To run Postgres you can use this predefined yaml, after addnig this repository to Argo-CD's repositories.
```yaml
apiVersion: argoproj.io/v1alpha1
kind: Application
metadata:
  name: postgres
spec:
  destination:
    name: ''
    namespace: postgres
    server: 'https://kubernetes.default.svc'
  source:
    path: postgres
    repoURL: 'https://github.com/amalic/kubernetes-argocd'
    targetRevision: HEAD
  sources: []
  project: default
  syncPolicy:
    automated:
      prune: false
      selfHeal: false
```