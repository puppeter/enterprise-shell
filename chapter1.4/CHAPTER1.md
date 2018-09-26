## 内建命令与外部命令

Linux命令有内建命令(内部命令）和外部命令之分，内部命令和外部命令功能基本相同，但也有些细微差别。

内建命令,实际上是Shell程序的一部分，其中包含的是一些比较简单的Linux系统命令，这些命令由Shell程序识别并在Shell程序内部完成运行，通常在Linux系统加载运行时shell就被加载并驻留在系统内存中。内部命令是写在bash源码里面的，其执行速度比外部命令快，因为解析内部命令Shell不需要创建子进程。比如：exit，history，cd，echo等，更多的内建命令使用见https://www.gnu.org/software/bash/manual/html_node/Builtin-Index.html#Builtin-Index。

外部命令,Linux系统中的实用程序部分，因为实用程序的功能通常都比较强大，所以其包含的程序量也会很大，在系统加载时并不随系统一起被加载到内存中，而是在需要时才将其调用内存。通常外部命令的实体并不包含在Lhell中，但是其命令执行过程是由Shell程序控制的。Shell程序管理外部命令执行的路径查找、加载存放，并控制命令的执行。外部命令是在Bash之外额外安装的，通常放在/bin，/usr/bin，/sbin，/usr/sbin......等等。可通过“echo $PATH”命令查看外部命令的存储路径，比如：ls、vi等。

我们可以通过type命令来识别内建命令还是外部命令。

```
[root@blog.puppeter.com_centos ~]#  type test    # 内建命令
test is a shell builtin

[root@blog.puppeter.com_centos ~]# type df    # 外部命令
df is /usr/bin/df
```



