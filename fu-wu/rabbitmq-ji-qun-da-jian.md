# rabbitmq集群搭建

## 镜像拉取

`docker pull rabbitmq:3.7-management`

## 创建rabbitmq运行目录

```text
mkdir rabbitmqcluster
cd rabbitmqcluster/
mkdir rabbitmq01 rabbitmq02 rabbitmq03
```

## 创建rabbitmq集群节点

```text
docker run -d --hostname rabbitmq01 --name rabbitmqCluster01 -v /home/software/rabbitmqcluster/rabbitmq01:/var/lib/rabbitmq -p 15672:15672 -p 5672:5672 -e RABBITMQ_ERLANG_COOKIE='rabbitmqCookie' rabbitmq:3.7-management
docker run -d --hostname rabbitmq02 --name rabbitmqCluster02 -v /home/software/rabbitmqcluster/rabbitmq02:/var/lib/rabbitmq -p 15673:15672 -p 5673:5672 -e RABBITMQ_ERLANG_COOKIE='rabbitmqCookie' --link rabbitmqCluster01:rabbitmq01 rabbitmq:3.7-management
docker run -d --hostname rabbitmq03 --name rabbitmqCluster03 -v /home/software/rabbitmqcluster/rabbitmq03:/var/lib/rabbitmq -p 15674:15672 -p 5674:5672 -e RABBITMQ_ERLANG_COOKIE='rabbitmqCookie' --link rabbitmqCluster01:rabbitmq01 --link rabbitmqCluster02:rabbitmq02 rabbitmq:3.7-management 
```

将mq2、mq3加入到集群中，并初始化

进入mq1

```text
docker exec -it rabbitmqCluster01 bash
rabbitmqctl stop_app
rabbitmqctl reset
rabbitmqctl start_app
exit
```

进入mq2

```text
docker exec -it rabbitmqCluster02 bash
rabbitmqctl stop_app
rabbitmqctl reset
rabbitmqctl join_cluster --ram rabbit@rabbitmq01
rabbitmqctl start_app
exit
```

进入mq3

```text
docker exec -it rabbitmqCluster03 bash
rabbitmqctl stop_app
rabbitmqctl reset
rabbitmqctl join_cluster --ram rabbit@rabbitmq01
rabbitmqctl start_app
exit
```

实现镜像模式集群。进入rabbitmqCluster01容器中

```text
docker exec -it rabbitmqCluster01 bash
rabbitmqctl set_policy-p/ha-all"^"'{"ha-mode":"all"}'
```



