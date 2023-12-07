This is a simple nginx application to demonstarte working with argocd ([readthedocs](https://argo-cd.readthedocs.io/en/stable/)).

[Tutorial](https://medium.com/@mehmetodabashi/installing-argocd-on-minikube-and-deploying-a-test-application-caa68ec55fbf)

Script:
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
