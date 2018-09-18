# 1.什么是Shell?

Shell是在Linux/UNIX下的命令解释型语言（command-language interpreter），它的中文翻译为“壳”主要是用于人机交互，以下截图为macOS中的Bash终端。

![](/assets/WX20180912-120240.png)

我们再来看一下Shell在Linux系统中的一个位置。从技术的角度来说Shell是一个使用者与系统的交互界面\(interface\), 只能让使用者通过命令行\(command line\)来使用系统来完成工作。 因此，Shell最简单的定义就是----命令解释器\( Command Interpreter\):

* 将使用者的命令翻译给kernel来处理；
* 同时，将kernel的处理结果翻译给使用者。

![](/assets/1.png)

# 2.Shell的种类

Linux Shell的种类很多，目前流行的Shell包括ash、bash、ksh、csh、zsh等，用户可以通过查看/etc/shells 文件中的内容来查看自己主机中当前有哪些种类的Shell。

```
cat /etc/shells
# List of acceptable shells for chpass(1).
# Ftpd will not allow users to connect who are not using
# one of these shells.
/bin/bash
/bin/csh
/bin/ksh
/bin/sh
/bin/tcsh
/bin/zsh
```

不同种类Shell间的历史背景:

* BourneShell\(sh\)：是由AT&T Bell实验室的 Steven Bourne为AT&T的Unix开发的，它是Unix的默认Shell，也是其它Shell的开发基础，Bourne Shell在编程方面相当优秀，但在处理与用户的交互方面不如其它几种Shell。
* BourneAgain Shell \(即Bash\)：是自由软件基金会\(GNU\)开发的一个Shell，它是Linux系统中一个默认的Shell。Bash不但与Bourne Shell兼容，还继承了C Shell、Korn Shell等优点。
* ash：ash Shell是由Kenneth Almquist编写的，是Linux 中占用系统资源最少的一个小Shell，它只包含24个内部命令，因而使用起来很不方便。
* CShell\(csh\)：是加州伯克利大学的Bill Joy为BSD Unix开发的，共有52个内部命令，与sh不同，它的语法与C语言很相似。它提供了Bourne Shell所不能处理的用户交互特征，如命令补全、命令别名、历史命令替换等。但是，C Shell与BourneShell并不兼容。该Shell其实是指向/bin/tcsh这样的一个Shell，也就是说，csh其实就是tcsh。
* KornShell\(ksh\)：是AT&T Bell实验室的David Korn开发的，共有42 条内部命令，它集合了C Shell和Bourne Shell的优点，并且与Bourne Shell向下完全兼容。Korn Shell的效率很高，其命令交互界面和编程交互界面都很好。
* zch：是Linux 最大的Shell之一，由Paul Falstad完成，共有84 个内部命令。如果只是一般的用途，没有必要安装这样的Shell。

大部分的Linux操作系统的预设Shell都是bash，其原因大致如下两种：

* 自由软件
* 功能强大 Bash是gnu project最成功的产品之一，自推出以来深受广大Linux/UNIX用户的喜爱， 且也逐渐成为不少组织的系统标准。

而目前互联网公司主流操作系统是CentOS，他默认的Shell就是Bash所以我们课程以介绍Bash为主，如果期间谈到其他Shell会以注释方式提示读者。

