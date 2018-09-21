和C语言类似，在Bash中用if、then、elif、else、fi这几条命令实现分支控制。

## 1.语法

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

# 或

if command ;then
    执行内容
fi
```

（**注：初学者一定要注意以上if..then语法中，条件语句两边都是有空格的，缺少一个空格都会报错且不容易被注意到。**）

## 2.案例

* 1.if..then的\[\]案例，比较两个值是否相等。

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

* 2.if..then的\(\(\)\)案例，比较两个值是否相等。

```
  #!/bin/bash
  i=100
  if ((10 <$i));then    # 数学比较方式
    echo "true"
  fi
```

* 3.if..command，判断是否为目录结构。

```
#!/bin/bash
dir=/home/
if cd "$dir" 2>/dev/null; then   # "2>/dev/null" 会隐藏错误信息.
    echo "Now in $dir."
    else  echo "Can't change to $dir."
fi
```



