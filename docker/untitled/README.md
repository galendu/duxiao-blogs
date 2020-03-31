# docker基础🎉

## 1.简介

## 2.安装

[win10 安装包下载地址](https://www.docker.com/get-started) 选择windows

#### linux 下安装docker

`vim docker-install.sh`

```text
#!/bin/bash
yum install -y yum-utils device-mapper-persistent-data lvm2
yum-config-manager --add-repo  https://mirrors.aliyun.com/docker-ce/linux/centos/docker-ce.repo
yum install -y docker-ce-18.06.0.ce-3.el7 
mkdir -p /etc/docker
tee /etc/docker/daemon.json <<-'EOF'
{
  "registry-mirrors": [
                       "https://iuj3d0uh.mirror.aliyuncs.com",
                       "http://hub-mirror.c.163.com",
                       "https://docker.mirrors.ustc.edu.cn",
                       "https://dockerhub.azk8s.cn",
                       "https://reg-mirror.qiniu.com",
                       "https://fz5yth0r.mirror.aliyuncs.com"
                        ],
  "graph": "/data/docker",
  "exec-opts": ["native.cgroupdriver=systemd"],
  "log-driver": "json-file",
  "log-opts": {
    "max-size": "100m",
    "max-file": "3",
    "labels": "production_status"
  },
  "storage-driver": "overlay2"
}
EOF

systemctl daemon-reload
systemctl enable docker
systemctl restart docker
```

执行脚本安装docker

`bash docker-install.sh`

## 3.配置

配置docker镜像加速器 vim /etc/docker/daemon.json

`docker-install.sh文件已配置,底下为镜像加速地址`

```text
"https://iuj3d0uh.mirror.aliyuncs.com",
"http://hub-mirror.c.163.com",
"https://docker.mirrors.ustc.edu.cn",
"https://dockerhub.azk8s.cn",
"https://reg-mirror.qiniu.com",
"https://fz5yth0r.mirror.aliyuncs.com",
"https://registry.docker-cn.com"
```

## 4.docker容器   _构建_   _**拉取**_   _运行_   过程如图所示

![](../../.gitbook/assets/image%20%286%29.png)

## 5.常见服务镜像dockerfile文件

java服务

python服务

nginx服务

更新中.....................

```text
。。。。。。。。。。。。。。。更新中
```

