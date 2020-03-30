# 入口网关服务注册发现-Openresty 动态 upstream

编辑Dockerfile文件

```text
FROM openresty/openresty:latest
LABEL maintainer="os4top16"
ADD ./openresty/ /etc/openresty/
```

使用方式

1.构建镜像

`docker build -t openresty-test:v1 .`

2.运行

```text
docker rm -f openresty
docker run -itd --name=openresty -p 800:800 -v ./openresty/:/etc/openresty/ openresty-test:v1
```

{% file src="../../.gitbook/assets/openresty.zip" caption="openresty文件" %}



