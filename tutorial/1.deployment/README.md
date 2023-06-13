## install
$ NAMESPACE=test
$ kubectl apply -f nginx.yaml -n $NAMESPACE


## 정리
$ kubectl delete -f nginx.yaml -n $NAMESPACE