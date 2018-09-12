# 1.编写第一个Shell脚本程序

这里我们来编写一个Shell程序，以在屏幕打印出hello world为例（起源[http://blog.puppeter.com/read.php?25](http://blog.puppeter.com/read.php?25)），vim编辑hello.sh内容如下。

```
#! /bin/bash              shell的命令解释器
# author:djangowang       标识脚本作者的名字
# time : 20180911         标识脚本开发的时间
# filename: hello.sh      标识脚本的名字
# 建议初学者每次写脚本按照以上的书写方式，优势是并行开发过程中能查到脚本的作者和开发时间，方便后续有问题的回溯
echo "hello wolrd"        #调用系统命令打印结果。
```

我们可以在Linux/Unix终端两种方式获取结果：
* 方式1： chmod 766 ./hello.sh  &&  ./hello.sh 执行打印结果。
* 方式2： /bin/sh ./hello.sh 执行打印结果。

最终都会在屏幕中打印出hello world。

# 2.Shell的注释功能
