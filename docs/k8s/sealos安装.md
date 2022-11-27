
```shell
yum -y install wget
```

```shell
wget  https://github.com/labring/sealos/releases/download/v4.1.3/sealos_4.1.3_linux_amd64.tar.gz  && \
    tar -zxvf sealos_4.1.3_linux_amd64.tar.gz sealos &&  chmod +x sealos && mv sealos /usr/bin 

sealos run labring/kubernetes:v1.24.1 labring/helm:v3.8.2 labring/calico:v3.24.1 --single
kubectl taint node --all node-role.kubernetes.io/control-plane-

sealos run labring/openebs:v1.9.0
```

verify
```shell
kubectl get nodes
```