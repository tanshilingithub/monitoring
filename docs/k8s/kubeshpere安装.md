
```shell

yum -y install net-tools
yum -y install conntrack-tools
yum -y install socat
```

install k8s on host
```shell
# Download KubeKey
curl -sfL https://get-kk.kubesphere.io | VERSION=v2.3.0 sh -
# Make kk executable
chmod +x kk
# Create a cluster
./kk create cluster --with-kubernetes v1.24.1 --container-manager containerd --with-kubesphere v3.3.0
```

install kubeshpere on k8s
```shell
kubectl apply -f https://github.com/kubesphere/ks-installer/releases/download/v3.3.1/kubesphere-installer.yaml
kubectl apply -f https://github.com/kubesphere/ks-installer/releases/download/v3.3.1/cluster-configuration.yaml
```

debug
```shell
kubectl logs -n kubesphere-system $(kubectl get pod -n kubesphere-system -l 'app in (ks-install, ks-installer)' -o jsonpath='{.items[0].metadata.name}') -f
kubectl -n kubesphere-system get pod|grep ks-installer|awk '{print $1}' | xargs kubectl -n kubesphere-system delete pod
kubectl -n kubesphere-system get pod
kubectl -n kubesphere-system describe pod ks-installer-746f68548d-gn24s
kubectl get pvc -A
kubectl get configmap -A
kubectl get pod -A|grep -v Running

kubectl -n kubesphere-system describe pod ks-apiserver-567fcb899d-msz6l
kubectl -n kubesphere-system describe pod ks-controller-manager-5d8b59b66f-fmwv2
kubectl -n kubesphere-system logs -f --tail 300 deploy/ks-apiserver

```

login
```shell
http://IP:30880   admin/P@88w0rd

```

调整prometheus部分
```shell
kubectl get pod -A|grep prometheus
kubectl -n kubesphere-monitoring-system edit pod prometheus-k8s-0
kubectl -n kubesphere-monitoring-system get config
kubectl -n kubesphere-monitoring-system get secret

kubectl -n kubesphere-monitoring-system edit secret prometheus-k8s
kubectl -n kubesphere-monitoring-system edit prometheus k8s
kubectl -n kubesphere-monitoring-system get svc
kubectl -n kubesphere-monitoring-system edit svc prometheus-k8s
  NodePort
```

visit:
http://192.168.186.132:30654
    查询出的一个cpu指标结果如下:
        node_cpu_guest_seconds_total{container="kube-rbac-proxy", cpu="0", instance="localhost.localdomain", job="node-exporter", mode="nice", namespace="kubesphere-monitoring-system", pod="node-exporter-c5sz2"}


