Howto:
- Add this repository to ArgoCD
- Create a new App called `postgres`
  - select automatic deployment
  - select this repository
  - enter `postgres` as path
  - select the kubernetes cluster
  - enter `postgres` as namespace

from https://www.airplane.dev/blog/deploy-postgres-on-kubernetes