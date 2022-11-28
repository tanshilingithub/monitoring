
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
    grafana:        http://192.168.186.137:32325
    prometheus:     http://192.168.186.137:31998