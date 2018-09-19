##判断是否为目录
在if后面也不一定非得是test命令或者是用于条件判断的中括号结构[ ] 或 [[ ]]。
```
#!/bin/bash
# author:djangwoang
# filename:checkDir.sh

dir=/home/bozo

if cd "$dir" 2>/dev/null; then   # "2>/dev/null" 会隐藏错误信息.
    echo "Now in $dir."
    else  echo "Can't change to $dir."
fi
```