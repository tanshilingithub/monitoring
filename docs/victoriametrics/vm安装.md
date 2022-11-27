```shell

helm repo add vm https://victoriametrics.github.io/helm-charts/
helm repo update

helm show values vm/victoria-metrics-cluster > values.yaml
kubectl create ns vm
helm install victoria-metrics vm/victoria-metrics-cluster -f values.yaml -n vm
```

debug
```shell
kubectl -n vm get pod
```