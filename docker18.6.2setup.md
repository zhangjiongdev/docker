yum 加速
```
curl -o /etc/yum.repos.d/docker-ce.repo http://mirrors.aliyun.com/docker-ce/linux/centos/docker-ce.repo
yum clean all && yum makecache fast
```

安装docker 依赖组件
```
sudo yum install -y yum-utils device-mapper-persistent-data lvm2
```

安装 docker-ce-18.06.2
```
sudo yum -y install docker-ce-18.06.2.ce-3.el7 docker-ce-cli-18.06.2.ce-3.el7
systemctl start docker && systemctl enable docker
docker --version
```
选这个版本的docker的原因：https://kubernetes.io/docs/setup/production-environment/container-runtimes/#docker


修改容器默认子网（预防与工作环境子网冲突）
```
cat > /etc/docker/daemon.json << EOF
{
    "bip": "172.31.0.1/16"
}
EOF

systemctl daemon-reload && systemctl restart docker && systemctl enable docker
```