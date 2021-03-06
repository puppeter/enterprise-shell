## Bash中的特殊变量

在Bash中有一些特殊的变量，他们分别是：

* $0    当前脚本的文件名
* $\#    传递给脚本或函数的参数个数。
* $\*    传递给脚本或函数的所有参数。
* $@    传递给脚本或函数的所有参数。被双引号\(" "\)包含时，与 $\* 稍有不同，下面将会讲到。
* $?    上个命令的退出状态，或函数的返回值。
* $$    当前Shell进程ID。对于 Shell 脚本，就是这些脚本所在的进程ID。
* $!    最近一次执行命令的进程号

### 1.$0 变量

$0变量是显示当前的文件名,譬如以下脚本为test.sh。

```
#!/bin/bash
echo $0    # 打印test.sh脚本名
echo $(dirname $0)    # $0 还有一种用法就是通过dirname命令显示当前脚本所在的位置。
```

### 2.$\#变量

传递给脚本或函数的参数个数。

```
#!/bin/bash
echo $#    # 输出当前位置变量的个数。

if [ $# -ne 3 ];then    # 位置变量通常用于判断位置参数的个数
    echo "please input three parameter!"
fi
```

## 3.$\* 和$@变量

$_ 和 $@ 都表示传递给函数或脚本的所有参数，不被双引号\(" "\)包含时，都以"$1" "$2" … "$n" 的形式输出所有参数。  
但是当它们被双引号\(" "\)包含时，"$_" 会将所有的参数作为一个整体，以"$1 $2 … $n"的形式输出所有参数；"$@" 会将各个参数分开，以"$1" "$2" … "$n" 的形式输出所有参数,以下是区别的案例。

```
#!/bin/bash
echo "\$*=" $*
echo "\"\$*\"=" "$*"
echo "\$@=" $@
echo "\"\$@\"=" "$@"
echo "print each param from \$*"
for var in $*
do
    echo "$var"
done
echo "print each param from \$@"
for var in $@
do
    echo "$var"
done
echo "print each param from \"\$*\""
for var in "$*"
do
    echo "$var"
done
echo "print each param from \"\$@\""
for var in "$@"
do
    echo "$var"
done
```

## 4.$?变量

判断上一个命令或函数的返回状态，其中0表示成功，非0表示失败。

```
[root@blog.puppeter.com_centos ~]# ls abc    # 在Linux终端执行ls abc,其中abc文件不存在系统会包错
ls: abc: No such file or directory
[root@blog.puppeter.com_centos ~]# echo $?    # 这时我执行$?就会显示一个非0的数字，表示上一次命令执行失败
1
[root@blog.puppeter.com_centos ~]# ls /etc/passwd    # 查看/etc/passwd文件是否存在，很显然他存在
/etc/passwd
[root@blog.puppeter.com_centos ~]# echo $?   # 会返回一个0的值，表示上一个命令返回成功。
0
```

我们在写脚本的过程中也可通过exit函数来告诉系统当前脚本的执行状态，譬如以下案例。

```
#!/bin/bash
echo "hello world"
exit 0    # 表示成功执行此脚本，退出状态码为0
```

## 5.$$变量

显示当前进程ID,我们在Linux系统中每执行一次命令或一个脚本都会启动一次进程，而进程ID就相当于唯一识别进程的身份证号。

```
[root@blog.puppeter.com_centos ~]# echo $$    # 他会打印出当前echo执行过程中的进程ID
1307
```

如果我们写了一个程序是常驻内存的，可以把此进程ID写到程序的pid文件中来告诉当前程序运行过程中的进程ID值，其实这有点像Apache和Nginx，这两款WEB服务都会将当前进程的ID值写入自己的pid文件中，当我要重启或关闭时其实就是获取pid文件中的进程ID并发送KILL信号。


## 6.$!变量
将一程序放在系统后台，打印$!放在后台这个程序的pid。

```
[root@blog.puppeter.com_centos ~]# sh 2.sh &
[1] 57947
[root@blog.puppeter.com_centos ~]# echo $!
57947
```
