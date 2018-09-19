##计算器
通过条件语句实现的计算器。
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
    tmp=$((a+b))
elif [ "$b" == "-" ];then
    tmp=$((a-b))
elif [ "$b" == "*" ];then
    tmp=$((a*b))
elif [ "$b" == "/" ];then
    tmp=$((a/b))
else
    echo "please input + - * /"
fi

echo "result is:${tmp}"










```