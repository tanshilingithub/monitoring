
install
```shell
kubectl create -f /tmp/prometheus/v0.11.0/setup
kubectl apply -f /tmp/prometheus/v0.11.0
```

debug
```shell
kubectl -n monitoring get pod|grep -v Running
```