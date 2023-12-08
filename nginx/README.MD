To run NGINX you can use this predefined yaml, after addnig this repository to Argo-CD's repositories.
```yaml
apiVersion: argoproj.io/v1alpha1
kind: Application
metadata:
  name: nginx
spec:
  destination:
    name: ''
    namespace: nginx
    server: 'https://kubernetes.default.svc'
  source:
    path: nginx
    repoURL: 'https://github.com/amalic/kubernetes-argocd'
    targetRevision: HEAD
  sources: []
  project: default
  syncPolicy:
    automated:
      prune: false
      selfHeal: false
```