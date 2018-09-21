## 1.\[\]和\[\[\]\]符号

首先我们通过type命令来看一下\[\]和\[\[\]\]在Bash中是什么：

```
type "test" "[" "[["
test is a shell builtin    # 内建命令
[ is a shell builtin    # 内建命令
[[ is a reserved word    # 关键字
```

所以在Bash中\[\]等价于test命令,案例。

```
test -f /etc/passwd   && echo true    # 结果为true
[ -f /etc/passwd ] && echo  ture     # 结果为true
```

\[\]和\[\[\]\]符号。

```
[ 10 -gt 20 && 3 -eq 3 ]&&echo y||echo n    # 会报错
[[ 10 -gt 20 && 3 -eq 3 ]]&&echo y||echo n    # 正常执行
```

两个符号相比：

* 1.\[\[\]\]更通用一些，\[\]仅在Bash下有效
* 2.\[\]为Shell命令，所以比较操作符"&gt;" 与"&lt;"必须转义否则就变成IO改向操作符。在\[\[中"&lt;"与"&gt;"不需转义，案例如下
  ```
  if [[ "$a" < "$b" ]]
  if [ "$a" \< "$b" ]
  ```



