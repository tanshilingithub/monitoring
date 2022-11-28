```shell
sysctl -w kernel.hostname=$(hostname -I|awk '{print $1}')
yum -y install wget
```

为了兼容电脑网络环境不好的改动
```shell
cp /tmp/sealos/sealos_4.1.3_linux_amd64.tar.gz ~/sealos_4.1.3_linux_amd64.tar.gz
tar -zxvf sealos_4.1.3_linux_amd64.tar.gz sealos &&  chmod +x sealos && mv sealos /usr/bin
```

```shell
wget  https://github.com/labring/sealos/releases/download/v4.1.3/sealos_4.1.3_linux_amd64.tar.gz  && \
    tar -zxvf sealos_4.1.3_linux_amd64.tar.gz sealos &&  chmod +x sealos && mv sealos /usr/bin

sealos run labring/kubernetes:v1.24.1 labring/helm:v3.8.2 labring/calico:v3.24.1 --single
kubectl taint node --all node-role.kubernetes.io/control-plane-
kubectl taint nodes --all node-role.kubernetes.io/master:NoSchedule-
sealos run labring/openebs:v1.9.0
```

verify
```shell
kubectl get nodes
```