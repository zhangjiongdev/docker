

启动 registry
```
docker pull registry:2
docker run -d -p 5000:5000 --restart always --name registry registry:2
```


下载镜像到registry仓库
```
docker pull zhangjiongdev/kube-apiserver:v1.16.2
docker pull zhangjiongdev/kube-scheduler:v1.16.2
docker pull zhangjiongdev/kube-proxy:v1.16.2
docker pull zhangjiongdev/kube-controller-manager:v1.16.2-b

docker pull zhangjiongdev/etcd:3.3.15-0
docker pull zhangjiongdev/pause:3.1
docker pull zhangjiongdev/coredns:1.6.2

docker pull zhangjiongdev/calico_cni:v3.10.0
docker pull zhangjiongdev/calico_pod2daemon-flexvol:v3.10.0
docker pull zhangjiongdev/calico_node:v3.10.0
docker pull zhangjiongdev/calico_kube-controllers:v3.10.0



docker tag zhangjiongdev/kube-apiserver:v1.16.2 localhost:5000/kube-apiserver:v1.16.2
docker tag zhangjiongdev/kube-scheduler:v1.16.2 localhost:5000/kube-scheduler:v1.16.2
docker tag zhangjiongdev/kube-proxy:v1.16.2 localhost:5000/kube-proxy:v1.16.2
docker tag zhangjiongdev/kube-controller-manager:v1.16.2-b localhost:5000/kube-controller-manager:v1.16.2-b

docker tag zhangjiongdev/etcd:3.3.15-0 localhost:5000/etcd:3.3.15-0
docker tag zhangjiongdev/pause:3.1 localhost:5000/pause:3.1
docker tag zhangjiongdev/coredns:1.6.2 localhost:5000/coredns:1.6.2

docker tag zhangjiongdev/calico_cni:v3.10.0 localhost:5000/calico_cni:v3.10.0
docker tag zhangjiongdev/calico_pod2daemon-flexvol:v3.10.0 localhost:5000/calico_pod2daemon-flexvol:v3.10.0
docker tag zhangjiongdev/calico_node:v3.10.0 localhost:5000/calico_node:v3.10.0
docker tag zhangjiongdev/calico_kube-controllers:v3.10.0 localhost:5000/calico_kube-controllers:v3.10.0

docker push localhost:5000/kube-apiserver:v1.16.2
docker push localhost:5000/kube-scheduler:v1.16.2
docker push localhost:5000/kube-proxy:v1.16.2
docker push localhost:5000/kube-controller-manager:v1.16.2-b

docker push localhost:5000/etcd:3.3.15-0
docker push localhost:5000/pause:3.1
docker push localhost:5000/coredns:1.6.2

docker push localhost:5000/calico_cni:v3.10.0
docker push localhost:5000/calico_pod2daemon-flexvol:v3.10.0
docker push localhost:5000/calico_node:v3.10.0
docker push localhost:5000/calico_kube-controllers:v3.10.0


```

