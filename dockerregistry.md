设置私有registry镜像地址（当网络无法访问公共镜像的时候）
```
export privateregistry=54.189.xxx.xxx:5000
```

修改 docker pull 配置
```
cat > /etc/docker/daemon.json << EOF
{
    "bip": "172.31.0.1/16",
    "insecure-registries": [
        "$privateregistry"
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
docker pull $privateregistry/kube-apiserver:v1.16.0
docker pull $privateregistry/kube-controller-manager:v1.16.0
docker pull $privateregistry/kube-controller-manager:v1.16.0b
docker pull $privateregistry/kube-scheduler:v1.16.0
docker pull $privateregistry/kube-proxy:v1.16.0

docker pull $privateregistry/etcd:3.3.15-0
docker pull $privateregistry/pause:3.1
docker pull $privateregistry/coredns:1.6.2

docker pull $privateregistry/cni:v3.8.2
docker pull $privateregistry/pod2daemon-flexvol:v3.8.2
docker pull $privateregistry/kube-controllers:v3.8.2
docker pull $privateregistry/node:v3.8.2


docker tag $privateregistry/kube-apiserver:v1.16.0 localhost:5000/kube-apiserver:v1.16.0
docker tag $privateregistry/kube-controller-manager:v1.16.0 localhost:5000/kube-controller-manager:v1.16.0
docker tag $privateregistry/kube-controller-manager:v1.16.0b localhost:5000/kube-controller-manager:v1.16.0b
docker tag $privateregistry/kube-scheduler:v1.16.0 localhost:5000/kube-scheduler:v1.16.0
docker tag $privateregistry/kube-proxy:v1.16.0 localhost:5000/kube-proxy:v1.16.0

docker tag $privateregistry/pause:3.1 localhost:5000/pause:3.1
docker tag $privateregistry/etcd:3.3.15-0 localhost:5000/etcd:3.3.15-0
docker tag $privateregistry/coredns:1.6.2 localhost:5000/coredns:1.6.2

docker tag $privateregistry/cni:v3.8.2 localhost:5000/cni:v3.8.2
docker tag $privateregistry/pod2daemon-flexvol:v3.8.2 localhost:5000/pod2daemon-flexvol:v3.8.2
docker tag $privateregistry/kube-controllers:v3.8.2 localhost:5000/kube-controllers:v3.8.2
docker tag $privateregistr/node:v3.8.2 localhost:5000/node:v3.8.2


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

