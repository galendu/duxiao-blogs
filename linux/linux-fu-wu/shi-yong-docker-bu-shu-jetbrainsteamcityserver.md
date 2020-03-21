# 使用docker部署jetbrains/teamcity-server

```text
docker run -it --name teamcity-server-instance \
-v datadir:/data/teamcity_server/datadir \
-v logs:/opt/teamcity/logs \
-p 8188:8111 \
jetbrains/teamcity-server
```

