Bash程序调试有多种方式：
* 方法1：通过命令打印信息到标准输出或追加到文件中
* 方法2：Bash自带参数
* 方法3：set命令


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
set是Bash的内建命令,经常用于程序的调试，注以下案例部分参考了http://www.ruanyifeng.com/blog/2017/11/bash-set.html?utm_source=tool.lu。

我们来看一下-x和+x的用法,以下是打印1-5的数字，其中-x用于打开调试，+x用于关闭调试。在程序执行过程中会看到打印到3，4时前面会有+号打印出调试信息。
```
#!/bin/bash

echo "1"
echo "2"
set -x
echo "3"
echo "4"
set +x
echo "5"
```

set -u的用法。 以下程序会在屏幕上打印出bar,其中变量$a是一个不存在的变量默认不会打出。
```
#!/bin/bash
echo $a
echo bar
```
我们对程序稍做修改，增加set -u会发现当遇到不存在的变量时程序会报错（1.sh: line 4: a: unbound variable）。
```
#!/bin/bash
set -u
echo $a
echo bar
```

set -e的用法。以下案例foo是一个不存在的命令，执行时会报错(1.sh: line 2: foo: command not found)但是Bash会忽略这个错误继续往下执行。

```
#!/bin./bash
foo
echo bar
```
-e 的作用就是脚本出现了问题就立马终止执行。
```
#!/bin./bash
set -e 
foo
echo bar
```

