# 1.编写第一个Bash脚本程序

这里我们来编写一个Bash程序，以在屏幕打印出hello world为例\(注：[hello world的起源](http://blog.puppeter.com/read.php?25)\)，VIM编辑hello.sh内容如下。

```
#! /bin/bash Bash的命令解释器
# author:djangowang 标识脚本作者的名字
# time : 20180911 标识脚本开发的时间
# filename: hello.sh 标识脚本的名字
# 建议初学者每次写脚本按照以上的书写方式，优势是并行开发过程中能查到脚本的作者和开发时间，方便后续有问题的回溯

echo "hello wolrd"    # 调用系统命令打印结果。
```

我们可以在Linux/Unix终端两种方式获取结果：

* 方式1： chmod 766 ./hello.sh && ./hello.sh 执行打印结果。
* 方式2： /bin/sh ./hello.sh 执行打印结果。

最终都会在屏幕中打印出hello world。

# 2.Bash的注释功能

在Bash中“\#”代表注释的意思，Bash的注释分为两种分别为：

* 单行注释，以“\#”号表示。

  ```
  #!/bin/bash
  # 单行注释
  echo "please input your name"    # 请你输入账号
  echo "please input your password"    # 请你输入密码
  ```

* 多行注释，固定语法格式。

```
#!/bin/bash
<<COMMENT
    author：djangowang
    time: 2018098
    filename: hi.sh
COMMENT
```

或更简单的方式，使用"‘"。

```
#!/bin./bash
: '
    author：djangowang
    time: 2018098 
    filename: hi.sh
'
```



