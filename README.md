# Requirements
* k8s cluster, my case rancher-desktop

# Setup ArgoCD
## Install

```
kubectl create namespace argocd
kubectl apply -n argocd -f install-argocd.yaml
```
[From docs, but gives errors connecting to repos](https://github.com/argoproj/argo-cd/issues/4174)  
`kubectl apply -n argocd -f https://raw.githubusercontent.com/argoproj/argo-cd/stable/manifests/install.yaml`



## Login

```
kubectl port-forward service/argocd-server -n argocd 8080:8080
```

Login: admin
Password: `kubectl -n argocd get secret argocd-initial-admin-secret -o jsonpath="{.data.password}" | base64 -d`

[Accessing ArgoCD console](https://localhost:8080/)
[Change Password](https://localhost:8080/user-info)

# Test with apps

## Create namespace
```
kubectl create namespace production
```

## Install argocd defs
```
kubectl -n argocd apply --filename project.yaml
kubectl -n argocd apply --filename apps.yaml
````