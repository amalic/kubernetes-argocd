Howto
- Add this repository to ArgoCD
- Create a new App called `hasura`
  - select automatic deployment
  - select this repository
  - enter `hasura` as path
  - select the kubernetes cluster
  - enter `hasura` as namespace
- port-forward ther service `kubectl port-forward svc/hasura -n hasura 8081:80`
- go to [http://localhost:8081](http://localhost:8081)