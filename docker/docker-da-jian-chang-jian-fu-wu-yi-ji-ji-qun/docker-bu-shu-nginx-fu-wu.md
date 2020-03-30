# docker部署nginx服务

```text
docker run -itd --restart=always  --name=nginx -p 8080:80 -v /data/nginx/conf/:/etc/nginx/conf.d/  -v /data/nginx/html/:/usr/share/nginx/html  nginx
```

{% file src="../../.gitbook/assets/nginx.7z" caption="nginx相关文件" %}

