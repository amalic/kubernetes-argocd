This is a simple nginx application to demonstarte working with argocd.

[Tutorial](https://medium.com/@mehmetodabashi/installing-argocd-on-minikube-and-deploying-a-test-application-caa68ec55fbf)

Script:
```bash
minikube start
kubectl create ns argocd
kubectl apply -n argocd -f https://raw.githubusercontent.com/argoproj/argo-cd/stable/manifests/install.yaml
echo "waiting for argocd-server"
sleep 5
kubectl -n argocd wait --for=condition=ready pod -l app.kubernetes.io/name=argocd-server
PASSWORD=$(kubectl -n argocd get secret argocd-initial-admin-secret -o jsonpath="{.data.password}" | base64 -d; echo -n)
echo "\nvisit http://localhost:8080"
echo "user:     admin"
echo "password: $PASSWORD\n"
kubectl port-forward svc/argocd-server -n argocd 8080:443
```
