## 1. 调用系统命令符号 \`\` 与 $\(\)

在Linux中\`\`和$\(\)都是用来执行系统命令的符号。
```
#!/bin/bash
mem=`free -m`
disk=$(df -h)

echo $mem    
echo $disk
```
在Linux中两个符号各有优缺点还要看用户的应用场景：

* \`\`基本上可用在全部的Shell版本中使用其移植性比较高，但反单引号容易打错或看错。
* $\(\)并不是所有shell都支持啊。


## 2. \转义与\续行
在Linux中“\”有两种含义转意和换行。
* 转意通常是将Linux中的一些特殊符号转为本身含义。譬如在屏幕上打印command=`ls`。

```
#!/bin/bash
string="command=`ls`"    # 打印出ls执行结果
string=command=\`ls\`    # 转意后的效果。
```