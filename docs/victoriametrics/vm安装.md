```shell

helm repo add vm https://victoriametrics.github.io/helm-charts/
helm repo update

helm show values vm/victoria-metrics-single > values.yaml
kubectl create ns vm
helm install vmsingle vm/victoria-metrics-single -f values.yaml -n vm
helm upgrade vmsingle vm/victoria-metrics-single -f values.yaml -n vm
helm uninstall vmsingle -n vm
```

debug
```shell
kubectl -n vm get pod
kubectl -n vm describe pod vmsingle-victoria-metrics-single-server-0
kubectl -n vm logs -f --tail 300 vmsingle-victoria-metrics-single-server-0
kubectl -n vm get svc
kubectl -n vm edit svc vmsingle-victoria-metrics-single-server
  NodePort

kubectl -n vm get svc vmsingle-victoria-metrics-single-server -o yaml > svc-vmsingle-victoria-metrics-single-server.yaml
  vmsingle-victoria-metrics-single-server > vmsingle-victoria-metrics-single-server-out
  ClusterIP -> NodePort
kubectl apply -f svc-vmsingle-victoria-metrics-single-server.yaml
```

visit:
http://192.168.186.132:30243

查询条件:   container_cpu_usage_seconds_total{container="alertmanager", cpu="total"}
查询结果:   prometheus:
container_cpu_usage_seconds_total{container="alertmanager", cpu="total", id="/kubepods.slice/kubepods-burstable.slice/kubepods-burstable-pod227f02b6_a96b_4e11_b7a5_eef718cbb353.slice/cri-containerd-227ba8a45c619461d75a50f5d06d5b5147a2d6f334955f8696ba197e391bb54f.scope", image="docker.io/prom/alertmanager:v0.23.0", instance="192.168.186.132:10250", job="kubelet", metrics_path="/metrics/cadvisor", name="227ba8a45c619461d75a50f5d06d5b5147a2d6f334955f8696ba197e391bb54f", namespace="kubesphere-monitoring-system", node="localhost.localdomain", pod="alertmanager-main-0"}
查询结果:   vm:
container_cpu_usage_seconds_total{container="alertmanager", cpu="total", id="/kubepods.slice/kubepods-burstable.slice/kubepods-burstable-pod227f02b6_a96b_4e11_b7a5_eef718cbb353.slice/cri-containerd-227ba8a45c619461d75a50f5d06d5b5147a2d6f334955f8696ba197e391bb54f.scope", image="docker.io/prom/alertmanager:v0.23.0", instance="localhost.localdomain", job="kubernetes-nodes-cadvisor", kubernetes_io_arch="amd64", kubernetes_io_hostname="localhost.localdomain", kubernetes_io_os="linux", name="227ba8a45c619461d75a50f5d06d5b5147a2d6f334955f8696ba197e391bb54f", namespace="kubesphere-monitoring-system", pod="alertmanager-main-0"}
