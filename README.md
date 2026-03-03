# Hello World – ArgoCD GitOps Demo

A simple Hello World web app deployed on a local [kind](https://kind.sigs.k8s.io/) Kubernetes cluster using [ArgoCD](https://argo-cd.readthedocs.io/) for GitOps continuous delivery.

## Project Structure

```
.
├── app/
│   ├── Dockerfile       # nginx-based container image
│   └── index.html       # Hello World page
├── k8s/
│   ├── namespace.yaml   # hello-world namespace
│   ├── configmap.yaml   # HTML content served by nginx
│   ├── deployment.yaml  # 2-replica nginx deployment
│   └── service.yaml     # ClusterIP service
└── argocd/
    └── application.yaml # ArgoCD Application manifest
```

## How It Works

ArgoCD watches the `k8s/` directory in this repo. Any change pushed to `main` is automatically synced to the local kind cluster — no manual `kubectl apply` needed.

## Access the App

```bash
kubectl port-forward svc/hello-world -n hello-world 8080:80
# Open http://localhost:8080
```

## Access ArgoCD UI

```bash
kubectl port-forward svc/argocd-server -n argocd 8443:443
# Open https://localhost:8443
# Username: admin
# Password: kubectl -n argocd get secret argocd-initial-admin-secret -o jsonpath="{.data.password}" | base64 -d
```
