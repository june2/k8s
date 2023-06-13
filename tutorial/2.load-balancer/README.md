## install
$ kubectl apply -f https://k8s.io/examples/service/load-balancer-example.yaml

$ kubectl describe deployments hello-world

$ kubectl expose deployment hello-world --type=LoadBalancer --name=my-service

$ kubectl describe services my-service


## 정리
$ kubectl delete services my-service
$ kubectl delete deployment hello-world
