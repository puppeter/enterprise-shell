## 1.分支语句的语法
在Bash中分支语句通过case来实现，它的语法如下。
## 1.case 
case语法。
```
case 匹配内容 in
   条件1） 执行内容;;
   条件2） 执行内容;;
   条件3） 执行内容;;
   *)  执行内容;;
esac

##2.case案例
```
#!/bin/bash
name=`basename $0 .sh`
case $1 in
 s|start)
        echo "start..."
        ;;
 stop)
        echo "stop ..."
        ;;
 reload)
        echo "reload..."
        ;;
 *)
        echo "Usage: $name [start|stop|reload]"
        exit 1
        ;;
esac
exit 0
 ```
