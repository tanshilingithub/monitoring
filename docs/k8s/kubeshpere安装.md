
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
./kk create cluster --with-kubernetes v1.24.1 --container-manager containerd --with-kubesphere v3.3.1
```

install kubeshpere on k8s
```shell
kubectl apply -f https://github.com/kubesphere/ks-installer/releases/download/v3.3.1/kubesphere-installer.yaml

kubectl apply -f https://github.com/kubesphere/ks-installer/releases/download/v3.3.1/cluster-configuration.yaml
```

debug
```shell
kubectl logs -n kubesphere-system $(kubectl get pod -n kubesphere-system -l 'app in (ks-install, ks-installer)' -o jsonpath='{.items[0].metadata.name}') -f
```

login
```shell
http://IP:30880   admin/P@88w0rd

```