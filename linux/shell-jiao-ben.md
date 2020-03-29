# shell脚本

1. 通过for循环实现查看主机服务器的最近登录城市

```bash
for i in `cat ip.txt`;do curl http://ip-api.com/json/$i?|python -m json.tool|grep city ;done
```



