## 子Shell

子Shell或者叫子进程，是从父子进程的概念出发的，UNIX操作系统的进程从init进程开始其他均有其对应的子进程，就算是由于父进程先行结束导致的孤儿进程，也会被init领养使其父进程ID为1。在Bash中 通常会通过以下几种形式产生子进程：

* &，提交后台作业
* \|，管道
* \(\)，操作符
* 外部命令
  > 需要注意的是，在写Bash脚本过程中推荐_\*\*_使用Bash内建\(builtin\)命令，因为外部命令会forks一个子进程效率并不是很高。

### 子Shell案例

#### 案例1

使用（）操作符来创建子进程。

```
#!/bin/bash

echo "Father Shell is: $BASH_SUBSHELL"    # 打印父Shell的层次，为0
outervar=OUTER                            # 父Shell的变量outervar

(                                           # 利用圆括号结构创建子Shell
    echo "SubShell is: $BASH_SUBSHELL"        # 子Shell的层次为1
    (
        echo "GrandSubShell is: $BASH_SUBSHELL" # 孙Shell的层次为2
    ) 
    innervar=INNER                            # 子Shell的变量
    echo "innervar=$innervar"
    echo "outervar=$outervar"                 # outervar继承了符Shell所赋给它的值
)                                           # 回到父shell

echo "Father Shell is: $BASH_SUBSHELL"   

if [ -z "$innervar" ]                      # 子Shell中定义变量为空，则说明并没有获取子Shell中变量
then
  echo "The \$innervar is not defined in main body."
else
   echo "The \$innervar is defined in main body."
fi
```

#### 案例2

通过管道\| ，& 和（）方式组成命令组并实现并发执行的效果，譬如以下这个案例：

```
#!/bin/bash
(grep -r "root" /etc/* | sort > part1)       &       #与root关键字匹配的行，排序后输出到某文件
(grep -r "root" /usr/local/* | sort > part2) &
(grep -r "root" /lib/* | sort > part3)       &
wait                                                 #等待后台执行的作业全部完成
cat part1 part2 part3 | sort > parttotal
echo "Run time of this script is:$SECONDS"           #输出该脚本执行时间
```

#### 案例3

有的同学也会关心\(\)和{}的区别，其实他们都是对命令组执行：

相同点：

* \(\)和{}都是把一串的命令放在括号里面,并且命令之间用;号隔开执行

不同点：

* \(\)只是对一串命令重新开一个子Shell进行执行,{}对一串命令在当前Shell执行
* \(\)最后一个命令可以不用分号,{}最后一个命令要用分号

> 注意： 在使用{}时，{}与命令之间必须使用一个空格

看以下案例。

```
[root@blog.puppeter.com_centos ~]# A=1;echo $A;{ A=2; };echo $A
1
2
[root@blog.puppeter.com_centos ~]# A=1;echo $A;(A=2);echo $A
1
1
```



