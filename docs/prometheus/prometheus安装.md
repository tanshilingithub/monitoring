
install
```shell
kubectl create -f /local_file/prometheus/v0.11.0/setup
kubectl apply -f /local_file/prometheus/v0.11.0
kubectl apply -f /local_file/prometheus
```

debug
```shell
kubectl -n monitoring get pod
kubectl -n monitoring get pod|grep -v Running

kubectl -n monitoring get svc
```

visit:
    grafana:        http://grafana.local.tanshilin.com          admin/admin
    prometheus:     http://prom.local.tanshilin.com