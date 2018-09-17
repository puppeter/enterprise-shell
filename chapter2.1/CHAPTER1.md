和C语言类似，在Shell中用if、then、elif、else、fi这几条命令实现分支控制。这种流程控制语句本质上也是由若干条Shell命令 。

#1. if..then
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
```
（初学者一定要注意以上if..then语法中，条件语句两边都是有空格的，缺少一个空格都会报错且不容易被注意到。）

if..then的案例，比较两个值是否相等。
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

#2. if..then..else
if..then..else的语法：

```
#!/bin/bash
if [ 条件语句 ]；then    # 推荐书写方式
    执行内容
else
    执行内容2
fi
```
if..then的案例，比较两个值是否相等。
```
#!/bin/sh
a=10
b=20
if [ $a == $b ];then    # 如果if和then写在一行，需要通过;来进行分割
   echo "a is equal to b"
else
   echo "a is not equal to b"
fi
```

#3. if..then..elif
if..then..elif的语法：
```
if [ 条件语句 ]
then
    执行内容
elif [ 条件语句 ]
then
    执行内容
...
else
    执行内容
fi
```
if..then..elif的案例，比较两个值是否相等。
```
#!/bin/bash
a=10
b=20
if [ $a == $b ]
then
    echo "a is equal to b"
elif [ $a -gt $b ]
then
   echo "a is greater than b"
elif [ $a -lt $b ]
then
   echo "a is less than b"
else
   echo "None of the condition met"
fi
```

```








