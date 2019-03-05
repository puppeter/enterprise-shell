# Shell加密
我们在写一些系统脚本时经常会把密码写在脚本文件中这是相当不安全的，但很多场景又是必须的这时加密脚本就显得非常有必要。这里我们通过gzexe命令来加密脚本,它无需安装常见的Linux发行版本中会自带，使用方法也很简单。

以下为测试脚本。
```
#!/bin/bash
#filename: hello.sh
echo "hello world"
```
通过gzexe命令来加密hello.sh脚本。
```
[root@blog.puppeter.com_centos ~]# chmod 766 hello.sh
[root@blog.puppeter.com_centos ~]# gzexe hello.sh
```
这是目录下会生产两个文件hello.sh加密后的和hello.sh~加密前的文件。再次执行以下结果确认是否要输出的内容。
