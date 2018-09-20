在Bash中分支语句通过case来实现，它的语法如下。
## 1.case语法
case语法。
```
case 匹配内容 in
   条件1） 执行内容;;
   条件2） 执行内容;;
   条件3） 执行内容;;
   *)  执行内容;;
esac
```

##2.case案例
案例1,计算器。

```
#!/bin/bash
if [ $# -ne 3 ]
then
   echo "参数个数应该为3，例如：$0 1 + 2"
   exit 1;
fi

case $2 in
   +)
    echo "scale=2;$1+$3" | bc
    ;;
   -)
    echo "scale=2;$1-$3" | bc
    ;;
   \*)
    echo "scale=2;$1*$3" | bc
    ;;
   /)
    echo "scale=2;$1/$3" | bc
    ;;
   *)
    echo "$2 不是运算符" 
    ;;
esac
exit 0
```
案例2，位置参数。
```
#!/bin/bash
name=`basename $0 .sh`
case $1 in
 START|start)
        echo "start..."
        ;;
 STOP|stop)
        echo "stop ..."
        ;;
 RELOAD|reload)
        echo "reload..."
        ;;
 *)
        echo "Usage: $name [start|stop|reload]"
        exit 1
        ;;
esac
exit 0
```
