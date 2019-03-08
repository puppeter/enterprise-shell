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
[root@blog.puppeter.com_centos ~]# gzexe hello.s
hello.sh:		  -39.7%
```
这是目录下会产生两个文件hello.sh加密后的和hello.sh~加密前的。我们查看加密后的hello.sh文件内容。
```
[root@blog.puppeter.com_centos ~]# cat hello.sh
#!/bin/sh -
# compressed by gzexe
lines=19
prog=`/usr/bin/basename "$0"`
tmp=`/usr/bin/mktemp -d /tmp/gzexeXXXXXXXXXX` || {
/bin/echo "$prog: cannot create tmp dir"; exit 1
}
trap '/bin/rm -rf "$tmp"' 0
if /usr/bin/tail +$lines "$0" |
    /usr/bin/gzip -dc > "$tmp/$prog" 2> /dev/null; then
/bin/chmod u+x "$tmp/$prog"
"$tmp/$prog" ${1+"$@"}
ret=$?
else
/bin/echo "$prog: cannot decompress $0"
ret=1
fi
exit $ret
*)?\1.shSV?O???OJ,?P?RVH??I?K?M?R?H????+??JM??WPs??rR???\o5
```
查看加密后hello.sh文件的执行结果。
```
[root@blog.puppeter.com_centos ~]#./hello.sh
hello world
```

