配置免密
```shell
# 生成证书文件(master)
ssh-keygen
cat /root/.ssh/id_rsa.pub >> /root/.ssh/authorized_keys
systemctl restart sshd
mkdir -p /local_file/ssh
/bin/cp -rf /root/.ssh/id_rsa.pub /local_file/ssh/id_rsa.pub
/bin/cp -rf /root/.ssh/id_rsa     /local_file/ssh/id_rsa



# 使用证书文件(slaver)
ls -alh /local_file/ssh/id_rsa.pub  /local_file/ssh/id_rsa
mkdir -p /root/.ssh
/bin/cp -rf /local_file/ssh/id_rsa.pub /root/.ssh/id_rsa.pub
/bin/cp -rf /local_file/ssh/id_rsa     /root/.ssh/id_rsa
cat /root/.ssh/id_rsa.pub >> /root/.ssh/authorized_keys
systemctl restart sshd
```

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

```shell
sealos gen labring/kubernetes:v1.24.1 labring/helm:v3.8.2 labring/calico:v3.24.1 \
  --masters 192.168.186.184,192.168.186.185,192.168.186.186 \
  --nodes   192.168.186.187,192.168.186.188,192.168.186.189 \
  > Clusterfile


sealos apply -f Clusterfile
sealos run labring/openebs:v1.9.0
```

划分节点池
```shell

```

verify
```shell
kubectl get nodes
```