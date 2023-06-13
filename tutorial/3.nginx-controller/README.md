## 설치 
```
$ NAMESPACE=ingress-basic
$ helm repo add ingress-nginx https://kubernetes.github.io/ingress-nginx
$ helm repo update
$ helm install ingress-nginx ingress-nginx/ingress-nginx --create-namespace --namespace $NAMESPACE --set controller.service.annotations."service\.beta\.kubernetes\.io/azure-load-balancer-health-probe-request-path"=/healthz
```

```
$ kubectl apply -f deploy-one.yml deploy-two.yml -n ingress-basic
$ kubectl apply -f nginx-ingress.yml -n ingress-basic
$ kubectl get ingress -n ingress-basic
```

## 확인
```
$ kubectl get pods -o wide --namespace ingress-basic
$ kubectl get services -o wide --namespace ingress-basic
$ kubectl describe ingress hello-world-ingress  --namespace ingress-basic
```