---
description: expect实现非交互式登录远程服务器
---

# expect脚本

```text
#!/bin/expect
spawn ssh root@192.168.0.23

expect {
    "yes/no" { send "yes\r"; exp_continue }
    "password:" {send "centos\r"};
}
interact
```

