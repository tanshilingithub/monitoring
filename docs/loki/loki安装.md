
```shell
helm repo add grafana https://grafana.github.io/helm-charts
helm install loki-distributed grafana/loki-distributed -n log-loki --create-namespace
helm uninstall loki-distributed -n log-loki
```

debug
```shell
kubectl -n log-loki get pod -o wide
kubectl -n log-loki get svc
```

integrate
```shell


```