## 1.语法

if..then..elif..fi的语法：

```
if [ 条件语句 ]；then
    执行内容
elif [ 条件语句 ]；then
    执行内容
else
    执行内容
fi

# 或

if [ 条件语句 ]
then
    执行内容
elif [ 条件语句 ]
then
    执行内容
else
    执行内容
fi
```

## 2.案例

1.if..then..elif..fi的案例，比较两个值是否相等。

```
#!/bin/bash
a=10
b=20
if [ $a -eq $b ]
then
    echo "a is equal to b"
elif [ $a -gt $b ]    # a 大于 b 见表1
then
   echo "a is greater than b"
elif [ $a -lt $b ]    # a 小于 b 见表1
then
   echo "a is less than b"
else
   echo "None of the condition met"
fi
```

文件比较符，表1。

| \[ \]括号 | （（））扩容 | 含义 |
| :--- | :--- | :--- |
| -eq | == | 等于 |
| -ne | != | 不等于 |
| -gt | &gt; | 大于 |
| -ge | &gt;= | 大于等于 |
| -lt | &lt; | 小于 |
| -le | &lt;= | 小于等于 |

2.通过条件语句实现的计算器。

```
#!/bin/bash
# author:djangwoang
# filename:jisuanqi.sh

echo "please input your first number"
read a
echo "please input + - * /"
read b
echo "please input your second number"
read c

if [ "x$b" == "x" ];then
    echo "please input + - * /"
elif [ "$b" == "+" ];then
    tmp=$((a+c))
elif [ "$b" == "-" ];then
    tmp=$((a-c))
elif [ "$b" == "*" ];then
    tmp=$((a*c))
elif [ "$b" == "/" ];then
    tmp=$((a/c))
else
    echo "please input + - * /"
fi

echo "result is:${tmp}"
```



