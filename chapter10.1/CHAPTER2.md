## Bash的生命周期

让我们来了解一下Bash从开始到、执行过程到结束它是什么一个过程。

### Bash的开始

目前我们已经比较了解Bash脚本编程了，一个脚本程序的开始方式都比较统一，它们几乎都开始于一个\#!符号。这个符号的作用大家似乎也都知道，叫做声明解释器。脚本语言跟编译型语言的不一样之处主要是脚本语言需要解释器。因为脚本语言主要是文本，而系统中能够执行的文件实际上都是可执行的二进制文件，就是编译好的文件。文本的好处是人看方便，但是操作系统并不能直接执行，所以就需要将文本内容传递给一个可执行的二进制文件进行解析，再由这个可执行的二进制文件根据脚本的内容所确定的行为进行执行。可以做这种解析执行的二进制可执行程序都可以叫做解释器。

脚本开头的\#!就是用来声明本文件的文本内容是交给那个解释器进行解释的。比如我们写bash脚本，一般声明的方法是\#!/bin/bash或\#!/bin/sh。如果写的是一个python脚本，就用\#!/usr/bin/python。当然，在不同环境的系统中，这个解释器放的路径可能不一样，所以固定写一个路径的方式就可能造成脚本在不同环境的系统中不通用的情况，于是就出现了这样的写法：

```
#!/usr/bin/env 脚本解释器名称
```

这就利用了env命令可以得到可执行程序执行路径的功能，让脚本自行找到在当前系统上到底解释器在什么路径。让脚本更具通用性。但是大家有没有想过一个问题，大多数脚本语言都是将\#后面出现的字符当作是注释，在脚本中并不起作用。这个\#!和这个注释的规则不冲突么？

这就要从\#!符号起作用的原因说起，其实也很简单，这个功能是由操作系统的程序载入器做的。在Linux操作系统上，出了1号进程以外，我们可以认为其它所有进程都是由父进程fork出来的。所以对bash来说，所谓的载入一个脚本执行，无非就是父进程调用fork\(\)、exec\(\)来产生一个子进程。这\#!就是在内核处理exec的时候进行解析的。

_内核中整个调用过程如下（linux 4.4），内核处理exec族函数的主要实现在fs/exec.c文件的do\_execveat\_common\(\)方法中，其中调用exec\_binprm\(\)方法处理执行逻辑，这函数中使用search\_binary\_handler\(\)对要加载的文件进行各种格式的判断，脚本（script）只是其中的一种。确定是script格式后，就会调用script格式对应的load\_binary方法：load\_script\(\)进行处理，\#!就是在这个函数中解析的。解析到了\#!以后，内核会取其后面的可执行程序路径，再传递给search\_binary\_handler（）重新解析。这样最终找到真正的可执行二进制文件进行相关执行操作。_

因此，对脚本第一行的\#!解析，其实是内核给我们变的魔术。\#!后面的路径内容在起作用的时候还没有交给脚本解释器。很多人认为\#!这一行是脚本解释器去解析的，然而并不是。了解了原理之后，也顺便明白了为什么\#!一定要写在第一行的前两个字符，因为这是在内核里写死的，它就只检查前两个字符。当内核帮你选好了脚本解释器之后，后续的工作就都交给解释器做了。脚本的所有内容也都会原封不动的交给解释器再次解释，是的，包括\#!。但是由于对于解释器来说，\#开头的字符串都是注释，并不生效，所以解释器自然对\#!后面所有的内容无感，继续解释对于它来说有意义的字符串去了。

### Bash执行过程

实际上bash在做这些功能的时候已经安排好了它们在名字冲突的情况下究竟该先以什么方式解释。优先顺序是：

* 别名：alias
* 关键字：keyword
* 函数：function
* 内建命令：built in
* 哈西索引：hash
* 外部命令：command

1.alias命令用来设置指令的别名。我们可以使用该命令可以将一些较长的命令进行简化。

```
[root@blog.puppeter.com_centos ~]# alias
alias cp='cp -i'
alias egrep='egrep --color=auto'
alias fgrep='fgrep --color=auto'
alias grep='grep --color=auto'
alias l.='ls -d .* --color=auto'
alias ll='ls -l --color=auto'
alias ls='ls --color=auto'
alias mv='mv -i'
alias rm='rm -i'
alias which='alias | /usr/bin/which --tty-only --read-alias --show-dot --show-tilde'
```

alias基本使用：

* 设置alias,新的命令='原命令 -选项/参数'
* 查看alias,alias -p
* 删除alias别名，unalias 命令名

2.keyword 关键字\(key word\)，譬如if，while，function等等。我们通过type来查看是否为关键字。

```
[root@blog.puppeter.com_centos ~]#  type function
function is a shell keyword
```

3.在判断为是否关键字后，Bash会再判断是否为函数\(function\)。

4.仅接着会判断是否为内建命令\(built in\)。

```
[root@blog.puppeter.com_centos ~]#  type alias
alias is a shell builtin
```

5.接着判断是否在hash索引。bash提供了一种功能，就是建立一个bash表，在第一次找到一个命令的路径之后，对其命令名和对应的路径建立一个hash索引。这样下次再执行这个命令的时候，就不用去遍历所有的目录了，只要查询索引就可以更快的找到命令路径，以加快执行程序的速度。

```
[root@blog.puppeter.com_centos ~]# hash
hits    command
   1    /bin/ls
```
最后是外部命令，外部命令主要搜索$PATH变量。

案例来源:[zooro的文章](https://mp.weixin.qq.com/s?__biz=MzIxNDMyODgyMA==&mid=2247483666&idx=1&sn=b3df5f3f8d8803fb88719463388db4ed&scene=0#wechat_redirect。)






