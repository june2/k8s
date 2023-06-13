## 설치 

- nginx ingress controller
https://docs.nginx.com/nginx-ingress-controller/installation/installation-with-helm/

```sh
$ NAMESPACE=ingress-basic
$ helm repo add ingress-nginx https://kubernetes.github.io/ingress-nginx
$ helm repo update
$ helm install ingress-nginx ingress-nginx/ingress-nginx --create-namespace --namespace $NAMESPACE --set controller.service.annotations."service\.beta\.kubernetes\.io/azure-load-balancer-health-probe-request-path"=/healthz
```

```sh
$ kubectl apply -f deploy-one.yml deploy-two.yml -n ingress-basic
$ kubectl apply -f nginx-ingress.yml -n ingress-basic
$ kubectl get ingress -n ingress-basic
```

## 확인
```sh
$ kubectl get pods -o wide --namespace ingress-basic
$ kubectl get services -o wide --namespace ingress-basic
$ kubectl describe ingress hello-world-ingress  --namespace ingress-basic
```