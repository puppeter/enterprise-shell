# 1.什么是Shell?

Shell是在Linux/UNIX下的命令解释型语言（command-language interpreter），它的中文翻译后为“壳”顾名思义主要是用于人机交互，以下截图为macOS中的Shell。

![](/assets/WX20180912-120240.png)

我们再来看一下以Shell在Linux系统中的一个位置，可以看到它介于用户和操作系统的中间层起到承上启下的作用。![](/assets/2.png)

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







