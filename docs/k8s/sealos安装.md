```shell
sysctl -w kernel.hostname=$(hostname -I|awk '{print $1}')
```

为了兼容电脑网络环境不好的改动
```shell
cp /local_file/sealos/sealos_4.1.3_linux_amd64.tar.gz ~/sealos_4.1.3_linux_amd64.tar.gz
tar -zxvf sealos_4.1.3_linux_amd64.tar.gz sealos &&  chmod +x sealos && mv sealos /usr/bin
```

```shell
yum -y install wget
wget  https://github.com/labring/sealos/releases/download/v4.1.3/sealos_4.1.3_linux_amd64.tar.gz  && \
    tar -zxvf sealos_4.1.3_linux_amd64.tar.gz sealos &&  chmod +x sealos && mv sealos /usr/bin

sealos run labring/kubernetes:v1.24.1 labring/helm:v3.8.2 labring/calico:v3.24.1 --single
kubectl taint node --all node-role.kubernetes.io/control-plane-
kubectl taint nodes --all node-role.kubernetes.io/master:NoSchedule-
kubectl taint nodes --all node.kubernetes.io/unreachable:NoSchedule-
sealos run labring/openebs:v1.9.0
#sealos run labring/ingress-nginx:4.1.0
```

verify
```shell
kubectl get nodes
#kubectl -n ingress-nginx get pod
#kubectl -n ingress-nginx logs -f --tail 300 ingress-nginx-admission-create-fq5gd
```