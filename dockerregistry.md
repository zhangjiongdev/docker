修改 docker pull 配置
```
cat > /etc/docker/daemon.json << EOF
{
    "bip": "172.31.0.1/16",
    "insecure-registries": [
        "54.189.172.225:5000"
    ]
}
EOF

systemctl daemon-reload && systemctl restart docker
```

启动 registry
```
docker run -d -p 5000:5000 --restart always --name registry registry:2
```


下载镜像到registry仓库
```
docker pull 54.189.172.225:5000/kube-apiserver:v1.16.0
docker pull 54.189.172.225:5000/kube-controller-manager:v1.16.0
docker pull 54.189.172.225:5000/kube-controller-manager:v1.16.0b
docker pull 54.189.172.225:5000/kube-scheduler:v1.16.0
docker pull 54.189.172.225:5000/kube-proxy:v1.16.0

docker pull 54.189.172.225:5000/etcd:3.3.15-0
docker pull 54.189.172.225:5000/pause:3.1
docker pull 54.189.172.225:5000/coredns:1.6.2

docker pull calico/cni:v3.8.2
docker pull calico/pod2daemon-flexvol:v3.8.2
docker pull calico/kube-controllers:v3.8.2
docker pull calico/node:v3.8.2


docker tag 54.189.172.225:5000/kube-apiserver:v1.16.0 localhost:5000/kube-apiserver:v1.16.0
docker tag 54.189.172.225:5000/kube-controller-manager:v1.16.0 localhost:5000/kube-controller-manager:v1.16.0
docker tag 54.189.172.225:5000/kube-controller-manager:v1.16.0b localhost:5000/kube-controller-manager:v1.16.0b
docker tag 54.189.172.225:5000/kube-scheduler:v1.16.0 localhost:5000/kube-scheduler:v1.16.0
docker tag 54.189.172.225:5000/kube-proxy:v1.16.0 localhost:5000/kube-proxy:v1.16.0

docker tag 54.189.172.225:5000/pause:3.1 localhost:5000/pause:3.1
docker tag 54.189.172.225:5000/etcd:3.3.15-0 localhost:5000/etcd:3.3.15-0
docker tag 54.189.172.225:5000/coredns:1.6.2 localhost:5000/coredns:1.6.2

docker tag calico/cni:v3.8.2 localhost:5000/cni:v3.8.2
docker tag calico/pod2daemon-flexvol:v3.8.2 localhost:5000/pod2daemon-flexvol:v3.8.2
docker tag calico/kube-controllers:v3.8.2 localhost:5000/kube-controllers:v3.8.2
docker tag calico/node:v3.8.2 localhost:5000/node:v3.8.2


docker push localhost:5000/kube-apiserver:v1.16.0
docker push localhost:5000/kube-controller-manager:v1.16.0
docker push localhost:5000/kube-controller-manager:v1.16.0b
docker push localhost:5000/kube-scheduler:v1.16.0
docker push localhost:5000/kube-proxy:v1.16.0

docker push localhost:5000/pause:3.1
docker push localhost:5000/etcd:3.3.15-0
docker push localhost:5000/coredns:1.6.2

docker push localhost:5000/cni:v3.8.2
docker push localhost:5000/pod2daemon-flexvol:v3.8.2
docker push localhost:5000/kube-controllers:v3.8.2
docker push localhost:5000/node:v3.8.2

```

