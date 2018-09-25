## 递归函数
递归函数既自己调用自己，以下这个案例就是通过递归函数实现或者叫递归炸弹，他可以不断的启动进程消耗系统资源直到系统死机为止。
```
:() { :|:& };:

或
.() { .|.& };.
```
如果不明白它上面意思，我们可以展开来看。
```
:()
{
:|: &
}
;
:

```
其实这里就是一个递归函数函数名为“:”它不断的自己调用自己启动进程，以下详细解释过程。

* 第一行行说明下面要定义一个函数，函数名为冒号":"，没有可选参数。
* 第二行表示函数体开始。
* 第三行是函数体真正要做的事情，首先它递归调用本函数，然后利用管道调用一个新进程（它要做的事情也是递归调用本函数），并将其放到后台执行。
* 第四行表示函数体结束。
* 第五行并不会执行什么操作，在命令行中用来分隔两个命令用。从总体来看，它表明这段程序包含两个部分，首先定义了一个函数，然后调用这个函数。
* 第六行表示调用本函数。 

那么如何防止这种炸弹函数对系统的威胁呢？ 我们可以通过ulimit系统命令限制用户的启动最大进程数来保护我们的系统，防止炸弹函数启动N多进程而耗尽系统资源。
```
[root@blog.puppeter.com_centos ~]# ulimit -u 709
[root@blog.puppeter.com_centos ~]# ulimit -a
core file size          (blocks, -c) 0
data seg size           (kbytes, -d) unlimited
file size               (blocks, -f) unlimited
max locked memory       (kbytes, -l) unlimited
max memory size         (kbytes, -m) unlimited
open files                      (-n) 4864
pipe size            (512 bytes, -p) 1
stack size              (kbytes, -s) 8192
cpu time               (seconds, -t) unlimited
max user processes              (-u) 709
virtual memory          (kbytes, -v) unlimited
```

关于炸弹函数更多请参考https://en.wikipedia.org/wiki/Fork_bomb。
