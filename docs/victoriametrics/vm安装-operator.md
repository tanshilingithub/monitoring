```shell
helm repo add vm https://victoriametrics.github.io/helm-charts/
kubectl create ns vm
helm install operator vm/victoria-metrics-operator -n vm
# helm uninstall vmoperator -n vm

kubectl create -n vm -f /tmp/victoriametrics/server.yaml
```
debug:
```shell
kubectl -n vm get pod
kubectl -n vm logs -f --tail 300 deploy/vmagent-example-vmagent vmagent
kubectl -n vm logs -f --tail 300 deploy/vminsert-example-vmcluster-persistent
kubectl -n vm logs -f --tail 300 vmselect-example-vmcluster-persistent-0
kubectl -n vm logs -f --tail 300 vmstorage-example-vmcluster-persistent-0
kubectl -n vm get svc|grep vmagent-example-vmagent
# 修改为外部访问
kubectl create -n vm -f /tmp/victoriametrics/vmagent-example-vmagent-out.yaml
```


visit vmagent: http://192.168.186.137:30755/targets


配置抓取(直接使用prometheus一整套即可, 同时排除掉prometheus本身)
```shell
kubectl create -f /tmp/prometheus/crd/
kubectl create -f /tmp/prometheus/serviceMonitor/
```

debug
```shell
kubectl -n vm get pod
kubectl -n vm describe pod vmsingle-victoria-metrics-single-server-0
# operator
kubectl -n vm logs -f --tail 300 deploy/vmoperator-victoria-metrics-operator

# single
kubectl -n vm logs -f --tail 300 vmsingle-victoria-metrics-single-server-0
kubectl -n vm get svc
kubectl -n vm edit svc vmsingle-victoria-metrics-single-server
  NodePort

kubectl -n vm get svc vmsingle-victoria-metrics-single-server -o yaml > svc-vmsingle-victoria-metrics-single-server.yaml
vi svc-vmsingle-victoria-metrics-single-server.yaml
  删除clusterIp几行
  vmsingle-victoria-metrics-single-server > vmsingle-victoria-metrics-single-server-out
  ClusterIP -> NodePort
kubectl apply -f svc-vmsingle-victoria-metrics-single-server.yaml
```

visit:
http://192.168.186.135:31441

查询条件:   container_cpu_usage_seconds_total{container="alertmanager", cpu="total"}
查询结果:   prometheus:
container_cpu_usage_seconds_total{container="alertmanager", cpu="total", id="/kubepods.slice/kubepods-burstable.slice/kubepods-burstable-pod227f02b6_a96b_4e11_b7a5_eef718cbb353.slice/cri-containerd-227ba8a45c619461d75a50f5d06d5b5147a2d6f334955f8696ba197e391bb54f.scope", image="docker.io/prom/alertmanager:v0.23.0", instance="192.168.186.132:10250", job="kubelet", metrics_path="/metrics/cadvisor", name="227ba8a45c619461d75a50f5d06d5b5147a2d6f334955f8696ba197e391bb54f", namespace="kubesphere-monitoring-system", node="localhost.localdomain", pod="alertmanager-main-0"}
查询结果:   vm:
container_cpu_usage_seconds_total{container="alertmanager", cpu="total", id="/kubepods.slice/kubepods-burstable.slice/kubepods-burstable-pod227f02b6_a96b_4e11_b7a5_eef718cbb353.slice/cri-containerd-227ba8a45c619461d75a50f5d06d5b5147a2d6f334955f8696ba197e391bb54f.scope", image="docker.io/prom/alertmanager:v0.23.0", instance="localhost.localdomain", job="kubernetes-nodes-cadvisor", kubernetes_io_arch="amd64", kubernetes_io_hostname="localhost.localdomain", kubernetes_io_os="linux", name="227ba8a45c619461d75a50f5d06d5b5147a2d6f334955f8696ba197e391bb54f", namespace="kubesphere-monitoring-system", pod="alertmanager-main-0"}
