## 空命令
在Bash中有一个命令为空命令":"，其实它什么也不能做只起到占位的作用，譬如以下案例判断/etc/passwd文件中是否存在root用户。
```
#!/bin/bash
if grep "root" /etc/passwd > dev/null ; do
    :    # 空命令在这只起到占位作用，如果没有空命令🈶会报错
else
    echo "user not exists"

done 
```
