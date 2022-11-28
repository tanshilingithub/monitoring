
install
```shell
kubectl create -f /tmp/prometheus/v0.11.0/setup
kubectl apply -f /tmp/prometheus/v0.11.0
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