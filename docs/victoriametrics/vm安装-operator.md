```shell
helm repo add vm https://victoriametrics.github.io/helm-charts/
#kubectl create ns vm
helm install operator vm/victoria-metrics-operator -n monitoring
# helm uninstall operator -n monitoring

#kubectl apply -n monitoring -f /local_file/victoriametrics/vmagent_rbac.yaml
#kubectl create -n monitoring -f /local_file/victoriametrics/vmagent_sa.yaml
kubectl apply -n monitoring -f /local_file/victoriametrics/server.yaml
kubectl apply -n monitoring -f /local_file/victoriametrics/ingress.yaml
```
```shell
#kubectl delete -n monitoring -f /local_file/victoriametrics/vmagent_rbac.yaml
kubectl delete -n monitoring -f /local_file/victoriametrics/server.yaml
kubectl delete -n monitoring -f /local_file/victoriametrics/ingress.yaml

```
debug:
```shell
kubectl -n monitoring get pod|grep vm
kubectl -n monitoring logs -f --tail 300 deploy/operator-victoria-metrics-operator
kubectl -n monitoring logs -f --tail 300 deploy/vmagent-example-vmagent vmagent
kubectl -n monitoring logs -f --tail 300 deploy/vminsert-example-vmcluster-persistent
kubectl -n monitoring logs -f --tail 300 vmselect-example-vmcluster-persistent-0
kubectl -n monitoring logs -f --tail 300 vmstorage-example-vmcluster-persistent-0
kubectl -n monitoring get svc|grep vmagent-example-vmagent

kubectl -n monitoring get deploy
kubectl -n monitoring get deploy vmagent-example-vmagent -o yaml
kubectl -n monitoring edit deploy vmagent-example-vmagent

kubectl -n monitoring get secret tls-assets-vmagent-example-vmagent -o yaml

kubectl -n monitoring get pod vmagent-example-vmagent-6d77694bdb-ngwc4 -o yaml

kubectl -n monitoring get configmap kube-root-ca.crt -o yaml
```


visit vmagent: http://vmagent-example-vmagent.local.tanshilin.com
integrate  vm: http://vmselect-example-vmcluster-persistent.vm:8481/select/0/prometheus/
