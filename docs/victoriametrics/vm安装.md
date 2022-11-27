```shell

helm repo add vm https://victoriametrics.github.io/helm-charts/
helm repo update

helm show values vm/victoria-metrics-single > values.yaml
kubectl create ns vm
helm install vmsingle vm/victoria-metrics-single -f values.yaml -n vm
helm uninstall vmsingle -n vm
```

debug
```shell
kubectl -n vm get pod
kubectl -n vm describe pod vmsingle-victoria-metrics-single-server-0
kubectl -n vm logs -f --tail 300 vmsingle-victoria-metrics-single-server-0
kubectl -n vm get svc
kubectl -n vm edit svc vmsingle-victoria-metrics-single-server
  NodePort

kubectl -n vm get svc vmsingle-victoria-metrics-single-server -o yaml > svc-vmsingle-victoria-metrics-single-server.yaml
  vmsingle-victoria-metrics-single-server > vmsingle-victoria-metrics-single-server-out
  ClusterIP -> NodePort
kubectl apply -f svc-vmsingle-victoria-metrics-single-server.yaml
```

visit:
http://192.168.186.132:30243