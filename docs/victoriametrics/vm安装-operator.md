```shell
helm repo add vm https://victoriametrics.github.io/helm-charts/
helm install operator vm/victoria-metrics-operator -n vm --create-namespace
# helm uninstall operator -n vm

#kubectl apply -n vm -f /local_file/victoriametrics/vmagent_rbac.yaml
#kubectl create -n vm -f /local_file/victoriametrics/vmagent_sa.yaml
kubectl apply -n vm -f /local_file/victoriametrics/server.yaml
kubectl apply -n vm -f /local_file/victoriametrics/ingress.yaml
```
```shell
#kubectl delete -n vm -f /local_file/victoriametrics/vmagent_rbac.yaml
kubectl delete -n vm -f /local_file/victoriametrics/server.yaml
kubectl delete -n vm -f /local_file/victoriametrics/ingress.yaml

```
debug:
```shell
kubectl -n vm get pod|grep vm
kubectl -n vm logs -f --tail 300 deploy/operator-victoria-metrics-operator
kubectl -n vm logs -f --tail 300 deploy/vmagent-example-vmagent vmagent
kubectl -n vm logs -f --tail 300 deploy/vminsert-example-vmcluster-persistent
kubectl -n vm logs -f --tail 300 vmselect-example-vmcluster-persistent-0
kubectl -n vm logs -f --tail 300 vmstorage-example-vmcluster-persistent-0
kubectl -n vm get svc|grep vmagent-example-vmagent

kubectl -n vm get deploy
kubectl -n vm get deploy vmagent-example-vmagent -o yaml
kubectl -n vm edit deploy operator-victoria-metrics-operator
kubectl -n vm edit deploy vmagent-example-vmagent

kubectl -n vm get secret tls-assets-vmagent-example-vmagent -o yaml

kubectl -n vm get pod vmagent-example-vmagent-6d77694bdb-ngwc4 -o yaml

kubectl -n vm get configmap kube-root-ca.crt -o yaml
```


```shell
kubectl -n vm logs -f --tail 300 deploy/vmagent-vm-vmagent vmagent
```

visit vmagent: http://vmagent-example-vmagent.local.tanshilin.com
integrate  vm: http://vmselect-example-vmcluster-persistent.vm:8481/select/0/prometheus/
