# 杂项命令

* eval命令
* wait命令
* trap命令

# eval命令

eval命令的格式eval command-line,其中command-line是终端上键入的一条普通命令，当前面放上eval时就会对Bash执行命令前进行两次扫描,譬如以下案例。

```
[root@blog.puppeter.com_centos ~]# pipe="|"
[root@blog.puppeter.com_centos ~]# ls $pipe wc -l
ls: -l: No such file or directory
ls: wc: No such file or directory
ls: |: No such file or directory
```

错误来源于ls,Bash在变量替换前处理了I/O重定向，因此不能知道pipe变量中的管道符号，结果就给ls传递了3个参数。这时我们可以使用eval。

```
[root@blog.puppeter.com_centos ~]# eval ls $pipe wc -l
    16
```

当Bash第一次扫描命令时会替换出pipe中的\|，接着eval使它再次扫描命令时，这时Bash把\|作为管道符号。不过建议不要过多的使用eval命令会导致脚本性能比较差。

# wait 命令

wait是用来阻塞当前进程的执行，直至指定的子进程执行结束后，才继续执行。使用wait可以在bash脚本“多进程”执行模式下，起到一些特殊控制的作用。

```
#!/bin/bash
sleep 10 &
wait # 等待10秒后，退出
exit 0
```

如果wait后面不带任何的进程号或作业号，那么wait会阻塞当前进程的执行，直至当前进程的所有子进程都执行结束后，才继续执行。

# trap命令

我们在运行脚本时如果无意按到了键盘上的按键或希望退出脚本时直接按ctrl+c会马上退出运行的程序，但是这里带来的问题就是会产生很多临时的数据问题。trap命令主要用来捕捉系统信号，当出现上述情况我们可以通过捕捉系统信号来做出相应的处理，譬如删除临时文件。

* 方式1，捕捉信号
* 方式2，无参数trap
* 方式3，忽略trap

trap捕捉信号有三种方式。

#### 方式1

trap "commands" signal-list 当脚本收到signal-list清单内列出的信号时,trap命令执行双引号中的命令。

```
#!/bin/bash
trap 'rm -rf /var/log/mess.log' INT    # 当捕捉到ctrl+c信号时，触发删除指定的文件
```

注：单引号和双引号是不同的，当shell程序第一次碰到trap语句时，将把commands中的命令扫描一遍。此时若commands是用单引号括起来的话，那么shell不会对commands中的变量和命令进行替换， 否则commands中的变量和命令将用当时具体的值来替换。

#### 方式2

执行无参数的trap是显示所有改过的陷阱。

```
 #!/bin/bash
trap 'echo logged off ' 0
trap
```

#### 方案3

如果列出的命令为空 ，当收到信号时就会忽略它。

```
#!/bin/bash
trap '' 2
while :
do
    :
done
```

我们可以通过kill命令或trap命令看到信号的列表和含义。以下以kill -l 为例大家还可以执行trap -l 最终的执行结果都是一样的没有太大区别。

```
[root@blog.puppeter.com_centos ~]# kill -l
 1) SIGHUP     2) SIGINT     3) SIGQUIT     4) SIGILL
 5) SIGTRAP     6) SIGABRT     7) SIGEMT     8) SIGFPE
 9) SIGKILL    10) SIGBUS    11) SIGSEGV    12) SIGSYS
13) SIGPIPE    14) SIGALRM    15) SIGTERM    16) SIGURG
17) SIGSTOP    18) SIGTSTP    19) SIGCONT    20) SIGCHLD
21) SIGTTIN    22) SIGTTOU    23) SIGIO    24) SIGXCPU
25) SIGXFSZ    26) SIGVTALRM    27) SIGPROF    28) SIGWINCH
29) SIGINFO    30) SIGUSR1    31) SIGUSR2
```



