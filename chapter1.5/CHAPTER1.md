## read命令
read是Bash的内建命令，主要用于从键盘读取内容赋值给变量，它有以下常用参数：
* -p :指定多个变量

```
#!/bin/bash

read -p “please input your name " name
echo "your name is $name" 
exit 0
```
* -n :计数输入的字符

```
#!/bin/bash

read -n6 -p “please input your password(lengh must be over 6 numbers)" passwd
exit 0
```

* -s :隐藏输入，不回显内容到终端

```
#!/bin/bash

read -s -n6 -p “please input your password(lengh must be over 6 numbers)" passwd
exit 0

```
* -t :超时等待时间

```
#!/bin/bash

read -t 5 -p “please input your name" name
if [ $? -eq 0 ];then
   echo "your name is $name" 
else
   echo "timeout"
fi
exit 0
```


