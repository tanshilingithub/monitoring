
```shell
yum -y install wget
export HTTP_PROXY="http://192.168.1.4:50579"
export HTTPS_PROXY="http://192.168.1.4:50579"
```

```shell
curl -LJO https://github.com/labring/sealos/releases/download/v4.1.3/sealos_4.1.3_linux_amd64.tar.gz && \
    tar -zxvf sealos_4.1.3_linux_amd64.tar.gz sealos &&  chmod +x sealos && mv sealos /usr/bin

sealos run labring/kubernetes:v1.25.0 labring/helm:v3.8.2 labring/calico:v3.24.1 --single
kubectl taint node --all node-role.kubernetes.io/control-plane-
sealos run labring/helm:v3.8.2
```