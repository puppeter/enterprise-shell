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
[root@blog.puppeter.com_centos ~]# eval ls $pipe wc -l
    16
```
错误来源于ls.
# wait 命令 
# trap命令

