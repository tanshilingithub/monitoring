
```shell
helm repo add grafana https://grafana.github.io/helm-charts
helm install loki-distributed grafana/loki-distributed -n loki --create-namespace
helm uninstall loki-distributed -n loki
```

debug
```shell
kubectl -n loki get pod -o wide

kubectl -n loki logs -f --tail 300 deploy/loki-distributed-distributor
kubectl -n loki logs -f --tail 300 deploy/loki-distributed-gateway
kubectl -n loki logs -f --tail 300 loki-distributed-ingester-0                       
kubectl -n loki logs -f --tail 300 loki-distributed-querier-0                        
kubectl -n loki logs -f --tail 300 deploy/loki-distributed-query-frontend


kubectl -n loki logs -f --tail 300 promtail-hl2t2

kubectl -n loki get svc
```

integrate
```shell
http://loki-distributed-gateway.loki:80
```

安装promtail
```shell
helm install promtail grafana/promtail -n loki --create-namespace -f values.yaml
```