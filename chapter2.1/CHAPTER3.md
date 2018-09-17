##1.[]和[[]]符号
首先我们通过type命令来看一下[]和[[]]在Bash中是什么：
``` 
type "test" "[" "[["
test is a shell builtin    # 内建命令
[ is a shell builtin    # 内建命令
[[ is a reserved word    # 关键字
```
所以在Bash中[]等价于test命令,案例。
```
test -f /etc/passwd   && echo true    # 结果为true
[ -f /etc/passwd ] && echo  ture     # 结果为true
```