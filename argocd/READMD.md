## 설치

```bash
kubectl create namespace argocd
kubectl apply -n argocd -f https://raw.githubusercontent.com/argoproj/argo-cd/stable/manifests/install.yaml
```

## WEB UI 접속

```bash
kubectl port-forward svc/argocd-server -n argocd 8080:443
```

## 비번셋업

```bash
kubectl -n argocd get secret argocd-initial-admin-secret -o jsonpath="{.data.password}" 
```