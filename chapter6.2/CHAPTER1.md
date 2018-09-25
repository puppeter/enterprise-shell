我们刚已经了解了函数的基本使用场景，很多时候函数用于节约我们的代码量，这里我们就用到了函数的加载。在Bash中函数有两种加载方式：
* "." 点
* source,Bash的内建命令
我们来看一下函数的应用场景，譬如我们有两个文件function.sh和test1.sh，其中functin.sh放了我们常用的函数，test1.sh是我们执行的脚本。

functin.sh内容。
```
# 加载系统环境变量
PATH=$PA TH:/usr/local/mysql/bin/:/Users/djangowang/wokrs/tools/clip/

checkDirectory(){
    $directorPath=$1
    if [ -d "$direcotryPath" ];then
        return "this is directory"
    else
        return "is not directory"
    fi
}
```
test1.sh内容.这里我们可以使用第一种加载方式也可以使用第二种加载方式。
```
#!/bin/bash
. function.sh    # 加载方式1
source function.sh    # 加载方式2

checkDirectory "/etc/passwd"

```