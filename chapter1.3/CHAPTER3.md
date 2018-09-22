在Bash中存在一些特殊符号，他们主要用于标准输出时的一些格式展现，如以下：  
特殊符号对照表，表1。

| 符号 | 含义 |
| :--- | :--- |
| \n | 新行 |
| \r | 回车 |
| \t | 制表符 |
| \v | 垂直的制表符 |
| \b | 后退符 |
| \a | 警告（蜂鸣或是闪动） |

在Bash中这些特殊符号主要用于以下两个命令的场景：

## 1.echo命令

echo命令是我们学习Bash编程中一个很常用的命令，他用于打印信息到标准输出，譬如。

```
[root@blog.puppeter.com_centos ~]#  echo "hello world"    # 打印hello world到标准输出
```

目前echo有两个参数：

* -n 不解析参数内的特殊符号
* -e 默认值，解析参数内的特殊符号

```
[root@blog.puppeter.com_centos ~]#  echo -n "hello\tworld"    # 不解析参数内制表符，同时不执行echo后的\n,特殊符号见表1
[root@blog.puppeter.com_centos ~]#  echo -e "hello\tworld"    # 解析参数中的制表符。
```

## 2.printf命令

我们再来看一下Printf命令。与echo相同的都是打印内容到屏幕上，但printf命令模仿 C 程序库（library里的 printf\(\) 程序，它由 POSIX 标准所定义，因此使用printf的脚本比使用echo移植性好,以下为案例。

```
#!/bin/bash
printf "%-10s %-8s %-4s\n" 姓名 性别 体重kg  
printf "%-10s %-8s %-4.2f\n" wds 男 66.1 
printf "%-10s %-8s %-4.2f\n" djangowang 男 77.6543 
printf "%-10s %-8s %-4.2f\n" hanmeimei 女 57.9876
```



