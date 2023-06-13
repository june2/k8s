## install
```sh
$ NAMESPACE=test
$ kubectl apply -f nginx.yaml -n $NAMESPACE
```

## 정리
```sh
$ kubectl delete -f nginx.yaml -n $NAMESPACE
```