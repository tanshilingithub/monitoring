
install
```shell
kubectl create -f /local_file/prometheus/v0.11.0/setup
kubectl apply -f /local_file/prometheus/v0.11.0
kubectl apply -f /local_file/prometheus
```

```shell

kubectl delete -f /local_file/prometheus/v0.11.0/prometheus-prometheus.yaml
```

debug
```shell
kubectl -n monitoring get pod
kubectl -n monitoring get pod|grep -v Running

kubectl -n monitoring get svc

kubectl -n monitoring logs -f --tail 300 prometheus-k8s-0
kubectl -n monitoring logs -f --tail 300 deploy/kube-state-metrics kube-state-metrics
kubectl -n monitoring edit deploy kube-state-metrics
kubectl -n monitoring get deploy kube-state-metrics -o yaml
kubectl -n monitoring logs -f --tail 300 deploy/grafana
kubectl -n monitoring get ingress
```

visit:
    grafana:        http://grafana.local.tanshilin.com          admin/admin
    prometheus:     http://prom.local.tanshilin.com


debug prometheus
```shell
kubectl -n monitoring get statefulset prometheus-k8s -o yaml
kubectl -n monitoring get pod prometheus-k8s-0 -o yaml
kubectl -n monitoring edit statefulset prometheus-k8s


kubectl -n monitoring get secret prometheus-k8s-web-config -o yaml
kubectl -n monitoring describe pod kube-state-metrics-6cd976fbf5-jf8dj
```