正则表达式，又称规则表达式。（英语：Regular Expression，在代码中常简写为regex、regexp或RE），计算机科学的一个概念。正则表达式通常被用来检索、替换那些符合某个模式\(规则\)的文本。

[https://github.com/wzb56/13\_questions\_of\_shell/blob/master/15.regular-expression.md](https://github.com/wzb56/13_questions_of_shell/blob/master/15.regular-expression.md)

# grep命令

因为本节正则大部分使用了grep命令，这里有必要介绍一下常用的两个参数：

* -E --extended-regexp
* -o --only-matching 只显示匹配的内容

# 基础的正则表示式

现在我们开始学习一些被称为元字符MetaCharacters的特殊字符。它们可以帮助我们创建更复杂的正则表达式搜索项。下面提到的是基本元字符的列表，

* ^ 匹配开头的字符
  ```
  [root@blog.puppeter.com_centos ~]# cat /etc/passwd | grep -E "^root"
  root:x:0:0:root:/root:/bin/bash
  
  [root@blog.puppeter.com_centos ~]# cat /etc/passwd | grep -E "root"
  root:x:0:0:root:/root:/bin/bash
  operator:x:11:0:operator:/root:/sbin/nologin
  dockerroot:x:994:991:Docker User:/var/lib/docker:/sbin/nologin
  ```
* $ 匹配结尾的字符
  ```
  [root@blog.puppeter.com_centos ~]# cat /etc/passwd | grep "root"
  root:x:0:0:root:/root:/bin/bash
  operator:x:11:0:operator:/root:/sbin/nologin
  dockerroot:x:994:991:Docker User:/var/lib/docker:/sbin/nologin
  
  [root@VM_99_152_centos ~]# cat /etc/passwd | grep "root" | grep "nologin$"
  operator:x:11:0:operator:/root:/sbin/nologin
  dockerroot:x:994:991:Docker User:/var/lib/docker:/sbin/nologin
  ```
* `.` 点将匹配任意字符
  ```
  [root@blog.puppeter.com_centos ~]# echo '1121、1122、112abc、1123131231' | grep -Eo '112.'
  1121
  1122
  112a
  1123
  ```
* `[ ]`将匹配一个字符范围,其中^表示取反
  ```
  [root@blog.puppeter.com_centos ~]#  echo "a b c d " \| grep -Eo '\[abc\]'
  a
  b
  c
  
  [root@blog.puppeter.com_centos ~]#  echo "a b c d " \| grep -Eo '\[^abc\]'
  d
  ```
* `*`将匹配零个或多个前面的项
  ```
  [root@blog.puppeter.com_centos ~]# echo "112、1122、1122222、1123131231" \| grep -Eo '1122\*'  
  112  
  1122  
  1122222  
  112
  ```
* `+`将匹配一个或多个前面的项
  ```
  [root@blog.puppeter.com_centos ~]# echo "abc abbc abbb" | grep -Eo 'ab+c'
  abc
  abbc
  ```
* `*`将匹配零个或多个前面的项
  ```
  [root@blog.puppeter.com_centos ~]# echo "112、1122、1122222、1123131231" \| grep -Eo '1122\*'  
  112  
  1122  
  1122222  
  112
  ```
* ?将匹配零个或一个前面的项
  ```
  [root@blog.puppeter.com_centos ~]# echo "ac abc " | grep -Eo 'ab?c'
  ac
  abc
  ```
* `{n}`将匹配 n 次前面的项
  ```
  [root@blog.puppeter.com_centos ~]# echo "abcdef aaacc aaca" | grep -Eo 'a{3}'
  aaa
  ```
* `{n,}`将匹配 n 次或更多前面的项
  ```
  [root@blog.puppeter.com_centos ~]# echo "abcdef aaacc aaaaca" | grep -Eo 'a{3,}'
  aaa
  aaaa
  ```
* `{n,m}`将匹配在 n 和 m 次之间的项
  ```
  [root@blog.puppeter.com_centos ~]# ifconfig | grep -Eo '[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}'
  127.0.0.1
  10.65.86.40
  10.65.86.255
  ```
* `\`是一个转义字符，当我们需要在我们的搜索中包含一个元字符时使用
  ```
  [root@blog.puppeter.com_centos ~]# echo "[]" | grep -Eo "\[\]"
  []
  ```



