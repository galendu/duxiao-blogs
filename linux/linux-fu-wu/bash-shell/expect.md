# expect

```text
#!/bin/expect
spawn ssh root@192.168.0.23

expect {
    "yes/no" { send "yes\r"; exp_continue }
    "password:" {send "centos\r"};
}
interact
```

