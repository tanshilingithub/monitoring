
```shell
yum -y install wget
wget  https://github.com/labring/sealos/releases/download/v4.1.3/sealos_4.1.3_linux_amd64.tar.gz  && \
    tar -zxvf sealos_4.1.3_linux_amd64.tar.gz sealos &&  chmod +x sealos && mv sealos /usr/bin
```
为了兼容电脑网络环境不好的改动
```shell
cp /local_file/sealos/sealos_4.1.3_linux_amd64.tar.gz ~/sealos_4.1.3_linux_amd64.tar.gz
tar -zxvf sealos_4.1.3_linux_amd64.tar.gz sealos &&  chmod +x sealos && mv sealos /usr/bin
```


配置免密
```shell
# 生成证书文件(master)
ssh-keygen
cat /root/.ssh/id_rsa.pub >> /root/.ssh/authorized_keys
systemctl restart sshd
mkdir -p /local_file/ssh
cp /root/.ssh/id_rsa.pub /local_file/ssh/id_rsa.pub
cp /root/.ssh/id_rsa     /local_file/ssh/id_rsa



# 使用证书文件(slaver)
ls -alh /local_file/ssh/id_rsa.pub  /local_file/ssh/id_rsa
mkdir -p /root/.ssh
cp -a /local_file/ssh/id_rsa.pub /root/.ssh/id_rsa.pub
cp -a /local_file/ssh/id_rsa     /root/.ssh/id_rsa
cat /root/.ssh/id_rsa.pub >> /root/.ssh/authorized_keys
systemctl restart sshd
```

```shell
sealos gen labring/kubernetes:v1.24.1 labring/helm:v3.8.2 labring/calico:v3.24.1 \
  --masters 192.168.186.154,192.168.186.155,192.168.186.156 \
  --nodes 192.168.186.154,192.168.186.155,192.168.186.156 \
  > Clusterfile



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