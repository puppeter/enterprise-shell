Bash程序调试有多种方式：
* 方法1：通过命令打印信息到标准输出或追加到文件中
* 方法2：Bash自带参数
* 方法3：set命令
* 方法4：使用"调试钩子"

## 方法1
我们可以通过echo和prinf命令将信息打印到标准输出或文件中。
```
#!/bin/bash
name=$1
pass=$2

echo $name   # 打印名字
echo $pass

if [ "$name" == "djangowang" -a "${pass}" == "123456" ];then
    echo "login succ"
fi

```


## 方法2
通过Bash自带参数：
* -x 跟踪模式(xtrace)。可以跟踪各种语法的调用，并打印出每个命令的输出结果
* -n 检测脚本是否有语法错误
* -v 可视模式，它会在执行bash程序的时候将要执行的内容也打印出来，除此之外，并不改变bash执行的过程：

见以下test.sh
```
#!/bin/bash
name=$1
pass=$2

if [ "$name" == "djangowang" -a "${pass}" == "123456" ];then
    echo "login succ"
fi

```

-v 执行结果。
```
[root@blog.puppeter.com_centos ~]#  sh -v test.sh djangowang 123456
#!/bin/bash
name=$1
pass=$2

if [ "$name" == "djangowang" -a "${pass}" == "123456" ];then
echo "login succ"
fi
login succ
```

-x 执行结果。
```
[root@blog.puppeter.com_centos ~]# sh -x  test.sh djangowang 123456
+ name=djangowang
+ pass=123456
+ '[' djangowang == djangowang -a 123456 == 123456 ']'
+ echo 'login succ'
login succ
```

## 方法3
set是Bash的内建命令
