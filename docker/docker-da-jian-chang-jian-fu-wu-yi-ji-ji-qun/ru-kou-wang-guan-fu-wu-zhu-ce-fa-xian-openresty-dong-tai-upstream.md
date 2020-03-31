# 入口网关服务注册发现-Openresty 动态 upstream

> OpenResty® 是一个基于 [Nginx](https://openresty.org/cn/nginx.html) 与 Lua 的高性能 Web 平台，其内部集成了大量精良的 Lua 库、第三方模块以及大多数的依赖项。用于方便地搭建能够处理超高并发、扩展性极高的动态 Web 应用、Web 服务和动态网关。
>
> OpenResty® 通过汇聚各种设计精良的 [Nginx](https://openresty.org/cn/nginx.html) 模块（主要由 OpenResty 团队自主开发），从而将 [Nginx](https://openresty.org/cn/nginx.html) 有效地变成一个强大的通用 Web 应用平台。这样，Web 开发人员和系统工程师可以使用 Lua 脚本语言调动 [Nginx](https://openresty.org/cn/nginx.html) 支持的各种 C 以及 Lua 模块，快速构造出足以胜任 10K 乃至 1000K 以上单机并发连接的高性能 Web 应用系统。
>
> OpenResty® 的目标是让你的Web服务直接跑在 [Nginx](https://openresty.org/cn/nginx.html) 服务内部，充分利用 [Nginx](https://openresty.org/cn/nginx.html) 的非阻塞 I/O 模型，不仅仅对 HTTP 客户端请求,甚至于对远程后端诸如 MySQL、PostgreSQL、Memcached 以及 Redis 等都进行一致的高性能响应。

### 1.这个方案中实现了3个接口，让 Openresty 支持添加、删除、监控 Upstream 后台节点的功能（如图接口1-接口3）

![](../../.gitbook/assets/image%20%285%29.png)

### 2.编辑Dockerfile文件并构建镜像，使用

```text
FROM openresty/openresty:latest

LABEL maintainer="os4top16 1610469455@qq.com"

ADD openresty/ /usr/local/openresty/
```

构建镜像

`docker build -t openresty-test:v1 .`

运行

```text
docker rm -f openresty
docker run -itd --name=openresty --restart=always -p 800:800 -v /data/openresty/:/usr/local/openresty/ openresty-test:v1
```

### 3.详解

openresty中包含三个脚本文件和openresty的主配置文件

#### 添加节点 

curl -v -X PUT '[http://192.168.0.59:800/ups?op=add&server=192.168.0.59:84](http://192.168.0.59:800/ups?op=add&server=192.168.0.59:84)'

#### 删除节点

curl -v -X PUT '[http://192.168.0.59:800/ups?op=del&server=192.168.0.59:84](http://192.168.0.59:800/ups?op=add&server=192.168.0.59:84)'

#### 监控节点

curl -v -X PUT '[http://192.168.0.59:800/ups?op=status&server=192.168.0.59:84](http://192.168.0.59:800/ups?op=add&server=192.168.0.59:84)' 

源配置文件只添加了三个节点，新添加节点需要在nginx.conf文件  
`server 192.168.0.59:86;`

![](../../.gitbook/assets/image%20%284%29.png)

{% file src="../../.gitbook/assets/openresty.zip" caption="openresty文件下载" %}

