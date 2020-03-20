---
description: centos7
---

# docker部署java服务

### 1.编写Dockerfile文件

```text
FROM openjdk:8-jdk-alpine
ARG JAVA_OPTS
ENV JAVA_OPTS=$JAVA_OPTS
VOLUME /app
WORKDIR /app
EXPOSE 1111   
RUN ln -sf /usr/share/zoneinfo/Asia/Shanghai /etc/localtime && echo 'Asia/Shanghai' >/etc/timezone
ADD xx.jar /app/xx/xx.jar
ENTRYPOINT exec java $JAVA_OPTS -jar -Duser.timezone=GMT+08 /app/xx/xx.jar
```

### 2.编写启动脚本

```text
#!/bin/bash
export VERSION=`date +%Y%m%d%H%M`
REGISTRY_USER=user
REGISTRY_PASSWORD="passwd"
PRE_REGISTER="镜像地址"
docker login --username=$REGISTRY_USER --password=$REGISTRY_PASSWORD $PRE_REGISTER && echo "登录阿里云仓库成功"
echo "******************************************************************************"
echo "开始docker化xx模块"
docker build -t $PRE_REGISTER/vip-bitqq-qqcmall/qqcmall-admin:xx-job . && echo "docker化成功"
echo "开始推送xx镜像"
docker push $PRE_REGISTER/模块名称/模块名称:$VERSION && echo "推送成功！"
docker rm -f xx
docker run -itd --name xx --network host --restart=always -v /app/logs:/app/logs $PRE_REGISTER/模块名称/模块名称:$VERSION
echo "******************************************************************************"
echo "=============== 开始部署到正式环境  ==============="
echo "$VERHISTORY$VERSION" >> versionhistory.txt
echo "版本号已经记录!"
```

