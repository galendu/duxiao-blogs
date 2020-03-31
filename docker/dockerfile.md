# dockerfile

### 1.了解ARG和FROM之间的交互方式

ARG CODE\_VERSION=latest  
FROM base:${CODE\_VERSION} 

### 2.RUN 执行命令，使用其它shell环境，请使用第三种方式传入所需的shell

1. RUN /bin/bash -c 'source $HOME/.bashrc; echo $HOME'
2. RUN /bin/bash -c 'source $HOME/.bashrc;echo $HOME'
3. RUN \["/bin/bash", "-c", "echo hello"\]
4. RUN echo "Hello world"

### 3.MAINTAINER 维护者

1. MAINTAINER os4top16
2. LABEL maintainer="os4top16@gmail.com"

### 4.LABEL 标签

* 父镜像（基础镜像）中包含的标签在新镜像中任然存在，创建重复的标签，则最近应用的值将会覆盖之前设置的值。可以使用docker inspect查看镜像中的标签
* LABEL "com.example.vendor"="ACME Incorporated" LABEL com.example.label-with-value="foo" LABEL version="1.0" LABEL description="This text illustrates  that label-values can span multiple lines."
* LABEL multi.label1="value1" multi.label2="value2" other="value3"
* LABEL multi.label1="value1" \

     multi.label2="value2" \

     other="value3"

### 5.EXPOSE 设置监听在指定的端口，默认tcp协议

* 要在运行容器时实际发布端口，请在docker run上使用-p标志发布并映射一个或多个端口，或使用-P标志发布所有公开的端口并将其映射到高阶端口（会随机指定端口），如例子3。
* EXPOSE 80/tcp
* EXPOSE 80/udp
* 使用-P标志发布所有公开的端口并将其映射到高阶端口

  ```bash
  [root@localhost data]# docker run -itd --name 03 -P nginx
  8f90cfdba786447a9445719a5ac1eed5272659c80664e9d1500a9951b8801ebb
  [root@localhost data]# docker ps
  CONTAINER ID        IMAGE                        COMMAND                  CREATED             STATUS              PORTS                              NAMES
  8f90cfdba786        nginx                        "nginx -g 'daemon of…"   3 seconds ago       Up 2 seconds        0.0.0.0:32768->80/tcp              03
  ```

### 6.ENV 创建环境变量 两种形式\(form\)

ENV   ENV = ... 1. ENV myName="John Doe" myDog=Rex The Dog  myCat=fluffy

1. ENV myName John Doe

   ENV myDog Rex The Dog

   ENV myCat fluffy

### 7.ADD 两种形式

ADD \[--chown=:\] ...  ADD \[--chown=:\] \["",... ""\]

ADD hom\* /mydir/ ADD hom?.txt /mydir/

ADD [https://firebasestorage.googleapis.com/v0/b/gitbook-28427.appspot.com/o/assets%2F-M0facU9lCTIfJSgNM-X%2F-M3iUnQMA0W2SW28aJz0%2F-M3icjxFY2\_\_cCFQ\_DIw%2Fopenresty.zip?alt=media&token=41f254a9-6527-4fe3-a099-3f1373802dd8](https://firebasestorage.googleapis.com/v0/b/gitbook-28427.appspot.com/o/assets%2F-M0facU9lCTIfJSgNM-X%2F-M3iUnQMA0W2SW28aJz0%2F-M3icjxFY2__cCFQ_DIw%2Fopenresty.zip?alt=media&token=41f254a9-6527-4fe3-a099-3f1373802dd8) /mydir/

ADD test relativeDir/ ADD test /absoluteDir/

1. ADD --chown=55:mygroup files\* /somedir/

   ADD --chown=bin files\* /somedir/

2. ADD --chown=1 files\* /somedir/

   ADD --chown=10:11 files\* /somedir/

### 8.COPY

COPY \[--chown=:\] ...  COPY \[--chown=:\] \["",... ""\]

1. COPY test relativeDir/   

   COPY test /absoluteDir/ 

COPY --chown=55:mygroup files _/somedir/ COPY --chown=bin files_ /somedir/ COPY --chown=1 files _/somedir/ COPY --chown=10:11 files_ /somedir/

### 9.ENTRYPOINT 可执行文件

ENTRYPOINT \["executable", "param1", "param2"\] \(exec form, preferred\) ENTRYPOINT command param1 param2 \(shell form\)

1. ENTRYPOINT \["top", "-b"\]

* $ docker run -it --rm --name test top -H

1. ENTRYPOINT exec top -b

* $ docker run -it --rm --name test top

### 10.VOLUME 创建具有指定名称的安装点

VOLUME /myvol

### 11.USER

USER \[:\] or USER \[:\]

USER yundd

### 12.WORKDIR 设置RUN,CMD,ENTRYPOINT,COPY和ADD 工作目录

1. WORKDIR /path/to/workdir
2. WORKDIR /a WORKDIR b WORKDIR c RUN pwd 

### 13.ONBUILD 已构建

ONBUILD ADD . /app/src ONBUILD RUN /usr/local/bin/python-build --dir /app/src

### 14.HEALTHCHECK 健康检查

HEALTHCHECK \[OPTIONS\] CMD command \(check container health by running a command inside the container\) HEALTHCHECK NONE \(disable any healthcheck inherited from the base image\)

--interval=DURATION \(default: 30s\) 间隔 --timeout=DURATION \(default: 30s\) 超时时间 --start-period=DURATION \(default: 0s\) 开始时间 --retries=N \(default: 3\) 重试

1. HEALTHCHECK --interval=5m --timeout=3s \

   CMD curl -f [http://127.0.0.1:800/](http://127.0.0.1:800/) \|\| exit 1

```bash
[root@localhost openresty]# docker ps
CONTAINER ID        IMAGE                        COMMAND                  CREATED             STATUS                             PORTS                              NAMES
2481edb4bfd5        yundd:v4                     "/usr/bin/openresty …"   21 seconds ago      Up 19 seconds (health: starting)   0.0.0.0:800->800/tcp               openresty
```

### 15.SHELL

SHELL \["executable", "parameters"\]

```bash
FROM microsoft/windowsservercore

# Executed as cmd /S /C echo default
RUN echo default

# Executed as cmd /S /C powershell -command Write-Host default
RUN powershell -command Write-Host default

# Executed as powershell -command Write-Host hello
SHELL ["powershell", "-command"]
RUN Write-Host hello

# Executed as cmd /S /C echo hello
SHELL ["cmd", "/S", "/C"]
RUN echo hello
```

