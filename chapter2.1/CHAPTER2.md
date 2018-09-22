## 1.语法

if..then..else..fi的语法：

```
#!/bin/bash
if [ 条件语句 ]；then    # 推荐书写方式
    执行内容
else
    执行内容2
fi

# 或

if [ 条件语句 ]
then
    执行内容
else
    执行内容2
fi
```

## 2.案例

1.if..then..else..fi的案例，比较两个值是否相等。

```
#!/bin/sh
a=10
b=20
if [ $a == $b ];then
   echo "a is equal to b"
else
   echo "a is not equal to b"
fi
```



