# 入口网关服务注册发现-Openresty 动态 upstream

> OpenResty® 是一个基于 [Nginx](https://openresty.org/cn/nginx.html) 与 Lua 的高性能 Web 平台，其内部集成了大量精良的 Lua 库、第三方模块以及大多数的依赖项。用于方便地搭建能够处理超高并发、扩展性极高的动态 Web 应用、Web 服务和动态网关。
>
> OpenResty® 通过汇聚各种设计精良的 [Nginx](https://openresty.org/cn/nginx.html) 模块（主要由 OpenResty 团队自主开发），从而将 [Nginx](https://openresty.org/cn/nginx.html) 有效地变成一个强大的通用 Web 应用平台。这样，Web 开发人员和系统工程师可以使用 Lua 脚本语言调动 [Nginx](https://openresty.org/cn/nginx.html) 支持的各种 C 以及 Lua 模块，快速构造出足以胜任 10K 乃至 1000K 以上单机并发连接的高性能 Web 应用系统。
>
> OpenResty® 的目标是让你的Web服务直接跑在 [Nginx](https://openresty.org/cn/nginx.html) 服务内部，充分利用 [Nginx](https://openresty.org/cn/nginx.html) 的非阻塞 I/O 模型，不仅仅对 HTTP 客户端请求,甚至于对远程后端诸如 MySQL、PostgreSQL、Memcached 以及 Redis 等都进行一致的高性能响应。

编辑Dockerfile文件

```text
FROM openresty/openresty:latest

LABEL maintainer="os4top16 1610469455@qq.com"

ADD openresty/ /usr/local/openresty/
```

使用方式

1.构建镜像

`docker build -t openresty-test:v1 .`

2.运行

```text
docker rm -f openresty
docker run -itd --name=openresty -p 800:800 -v ./openresty/:/usr/local/openresty/ openresty-test:v1
```

{% file src="../../.gitbook/assets/openresty.zip" caption="openresty文件" %}

3.详解

openresty中包含三个脚本文件，分别为srvcheck.lua upsops.lua upstream.lua 







