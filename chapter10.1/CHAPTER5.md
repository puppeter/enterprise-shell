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
当Bash第一次扫描命令时会替换出pipe中的|，接着eval使它再次扫描命令时，这时Bash把|作为管道符号。

# wait 命令 
wait是用来阻塞当前进程的执行，直至指定的子进程执行结束后，才继续执行。使用wait可以在bash脚本“多进程”执行模式下，起到一些特殊控制的作用。
```
#!/bin/bash
sleep 10 &
sleep 5&
wait #等待10秒后，退出
```
如果wait后面不带任何的进程号或作业号，那么wait会阻塞当前进程的执行，直至当前进程的所有子进程都执行结束后，才继续执行。

# trap命令

