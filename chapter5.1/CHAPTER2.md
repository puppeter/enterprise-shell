\#!/bin/bash -r\(restricted bash\)即受限制的bash,其可以用作中转服务器或者仅使用 ssh 来访问网页等等。我们可以用\#!/bin/bash -r或set -r方式运行Bash受限模式，开启受限模式后具体表现如下：

* 通过 cd 来改变工作目录
* 设置或取消环境变量： SHELL， PATH， ENV， BASH\_ENV
* 命令名中不能包含目录分隔符 ‘/’
* 包含有 ‘/’ 的文件名作为内置命令 ‘.’ 的参数
* hash 内置命令有 -p 选项时的文件名参数包含 '/'
* 在启动时通过 shell 环境导入函数定义
* 在启动时通过 shell 环境解析 SHELLOPTS 的值
* 使用 &gt;，&gt;\|， &lt;&gt;， &gt;&， &&gt;， &gt;&gt; 等重定向操作符
* 使用 exec 内置命令
* 通过 enable 内置命令的 -f 和 -d 选项增加或删除内置命令
* 使用 enable 内置命令来禁用或启用 shell 内置命令
* 执行 command 内置命令时加上 -p 选项
* 通过 set +r 或 set +o restricted 关闭受限模式
* 现在通过受限bash来创建只读用户。

开启Bash受限模式后会发现变得更安全，再来看一个案例通过set -r方式运行Bash限制模式。

```
#!/bin/bash

echo "Changing current work directory"
cd /etc
echo "Now in $PWD"

set -r
echo "------IN RESTRICTED MODE---------"
echo "Trying to change directory"
cd /usr/local
```

但要注意的是bash提供的受限环境的安全程度取决于用户能执行的命令，很多命令都能调用外部命令，从而导致逃逸出受限环境。例如用 vim 打开一个文件：

```
[root@blog.puppeter.com_centos ~]# vim /etc/passwd

然后执行外部命令：

[root@blog.puppeter.com_centos ~]# !bash
```

这样就可以启动一个不受限的bash，这对 more，less，man 等命令同样有效。如果还能执行脚本，如 python，perl 等，则有很多方式来启动一个不受限的 shell。要让bash受限模式更安全，可以限制用户能够执行的命令，如我们让用户执行执行 ssh 命令。一种方法是，修改 PATH 环境变量。例如我们创建一个user\_00用户，让他只能执行 ssh 命令：

```
[root@blog.puppeter.com_centos ~]# ls -s /bin/bash /bin/rbash
[root@blog.puppeter.com_centos ~]# useradd -s /bin/rbash user_00
[root@blog.puppeter.com_centos ~]# chown -R root:user_00 /home/user_00/.bashrc /home/user_00/.bash_profile
[root@blog.puppeter.com_centos ~]# chmod 640 /home/user_00/.bashrc /home/user_00/.bash_profile
[root@blog.puppeter.com_centos ~]# mkdir /home/user_00/bin
```

然后修改 PATH 环境变量的值为 /home/user\_00/bin，并将允许执行的命令放到这个目录下。：

```
[root@blog.puppeter.com_centos ~]# echo "export PATH=/home/user_00/bin" >> /home/user_00/.bash_profile
```

把用户可执行的命令链接到用户 PATH 路径下：

```
[root@blog.puppeter.com_centos ~]# $ ln -s /user/bin/ssh /home/ruser/bin/ssh
```

这样就可以只让登录的用户执行 ssh 命令。

