## 案例1
在写while循环的时候，发现了一个问题，在while循环内部对变量赋值、定义变量、数组定义等等环境，在循环外面失效，失效案例如下。
```
#!/bin/bash
echo "abc xyz" | while read line
do
    new_var=$line
done
echo new_var is null: $new_var?
```

原因，这使得while语句在子shell中执行，这意味着while语句内部设置的变量、数组、函数等在循环外部都不再生效。以下为解决方案。

```
#!/bin/bash
while read line
do
    new_var=$line
done <<< "abc xyz"
echo new_var is null: $new_var?
```
"<<<" 以这种方式直接在命令之前分配的变量仅对命令进程生效。

案例来源：https://www.cnblogs.com/f-ck-need-u/p/7431578.html

## 案例2 
今天在一些机器上批量执行命令，将10多个ip追加到指定文件中（ip）通过以下Shell方式来批量执行。

```
#!/bin/bash
while read line
do
         ssh $line "command"
done < ip
```

奇怪的是每次执行1行就退出。 网上google以下原因，while read 会从标准输入读取1行数据赋值给line变量，在while中循环嵌套ssh，ssh命令就会截取所有标准输入的数据这就导致read再次读数据时数据已经被ssh读取，line变量获取为空值最终导致循环结束。 

解决方式：
* 方案1：ssh -n ,其中-n参数含义如下：
-n 把 stdin 重定向到 /dev/null (实际上防止从 stdin 读取数据). 在后台运行时一定会用到这个选项. 它的常用技巧是远程运行 X11 程序. 例如, ssh -n shadows.cs.hut.fi emacs 将会在 shadows.cs.hut.fi 上启动 emacs, 同时自动在加密通道中转发 X11 连接. 在后台运行. (但是如果 要求口令或密语, 这种方式就无法工作; 参见 -f 选项.)

* 方案2：ssh "command" < /dev/null 
* 方案3：或者循环时使用for

案例来源：http://blog.puppeter.com/read.php?65