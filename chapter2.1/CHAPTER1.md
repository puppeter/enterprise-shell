和C语言类似，在Shell中用if、then、elif、else、fi这几条命令实现分支控制。这种流程控制语句本质上也是由若干条Shell命令 。

#if..then..fi
if..then的语法：
```
#!/bin/bash
if [ 条件语句 ]；then    # 推荐书写方式
    执行内容
fi
# 或
if [ 条件语句 ]
then
    执行内容
fi
# 或
if (());then
    执行内容
fi
```
（初学者一定要注意以上if..then语法中，条件语句两边都是有空格的，缺少一个空格都会报错且不容易被注意到。）

* if..then的[]案例，比较两个值是否相等。

```
#!/bin/sh
a=10
b=20
if [ $a == $b ];then    # 如果if和then写在一行，需要通过;来进行分割
   echo "a is equal to b"
fi

if [ $a != $b ]
then
   echo "a is not equal to b"
fi
```
* if..then的(())案例，比较两个值是否相等。
```
#!/bin/bash
i=100
if ((10 <$i));then    # 数学比较方式
    echo "true"
fi
```






