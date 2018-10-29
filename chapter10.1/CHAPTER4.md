# /bin/bash 和/bin/sh区别

脚本头通常是程序执行过程中的解释器。我们在编写脚本时脚本头常见的有两种书写方式。

```
#!/bin/bash
或
#!/bin/sh
```

注：当然还有一种熟悉方式\#!/usr/bin/env bash 这里暂时不做讨论。

那这两种方式有什么区别呢，我们来看网上的一个案例test.sh。

```
#!/bin/sh
source pcy.sh    # pcy.sh文件并不存在
echo hello


[root@blog.puppeter.com_centos ~]# ./test.sh
./test.sh: line 2: pcy.sh: No such file or directory
```

如果将/bin/sh改为/bin/bash,就会打印出hello。

```
#!/bin/bash
source pcy.sh    # pcy.sh文件并不存在
echo hello
[root@blog.puppeter.com_centos ~]# ./test.sh
./test.sh: line 2: pcy.sh: No such file or directory
hello
```

那sh和bash有什么区别呢？ 其实/bin/sh就是Linux系统中的一个软连接，他指向了/bin/bash并开启了--posix参数，所以他们的区别就是一个bash加载了--posix参数一个没有加载，关于posix模式对Bash的影响这里可以参考https://www.gnu.org/software/bash/manual/html\_node/Bash-POSIX-Mode.html。

