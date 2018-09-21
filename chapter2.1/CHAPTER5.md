## 字符串判断、与、或和非

在编写Bash程序过程中我们经常会用到判断字符串是否为空，这里可以通过-z和-n来直接判断。

* -z:字符串为null，即长度为0
* -n:字符串不为null，即长度不为0

案例：

```
# 判断字符串不为空
#!/bin/bash
string="hello world"
if [ -n "$string" ];then
    echo "true"
fi

# 判断字符串为空
#!/bin/bash
string=""
if [ -z "$string" ];then
    echo "true"
fi

# 判断字符串为空
#!/bin/bash
string=""
if [ x"$string" == "x" ];then
    echo "true"
fi
```

Bash中的与、或和非。

* -a 与
* -o 或
* ! 非

案例：

```
if [ ! -d /etc/passwd ];then # 如果这不是一个目录结果为真
    echo "it's not dirctory"
fi

if [ -e /var/log/messages -a -r /var/log/messages ];then # 如果文件存在同时又可读的情况下，表达式为真
    echo "true"
fi

if [ ! -e /etc/passwd -o -w /etc/passwd ];then # 如果文件不存在或者文件有写权限的情况下，表达式为真
    echo "true"
fi
```



