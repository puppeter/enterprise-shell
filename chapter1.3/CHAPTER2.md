##数学运算
Bash默认为字符串类型，我们可以通过以下几种方式在Bash中进行数学运算。
* 简单计算，(())、let和[]
* 高级计算, expr、bc



###1.（()）结构
通过(())结构进行数学运算,推荐方式。
```
#!/bin/sh
i=10
echo $i
i=$((i+10))    # 结果为20
echo $i
i=$((i+100))    # 结果为120
echo $i
```
(())还可以使用C风格来设置处理变量。
```
#!/bin/bash
(( a = 23 ))    # 以C风格来设置一个值，在"="两边可以有空格
echo "a (initial value) = $a"
(( a++ ))    # C风格的计算后自增
echo "a (after a++) = $a"
(( a-- ))    # C风格的计算后自减
echo "a (after a--) = $a"
(( ++a ))    # C风格的计算前自增
echo "a (after ++a) = $a"
(( --a ))    # C风格的计算前自减
echo "a (after --a) = $a"
```
(())还可用于进制转换。
```
# 八进制转十进制：
((num=0123));
echo $num;    # 结果83

((num=8#123));
echo $num;    # 结果83

# 十六进制转十进制：
((num=0xff)); 
echo $num;    # 结果255
((num=16#ff));
echo $num;    # 结果255

# 二进制转十进制
((num=2#11111111));  
echo $num;    # 结果255
```
###2.let内置命令
let是Bash中的内置命令，我们可以通过它来做数据运算。

```
#!/bin/sh
i=10
echo $i
let i=i+10    # 结果为20
echo $i
let "i=i+100"   # 结果为120
echo $i
```

###3.[] 结构
通过[]结构进行数学运算。

```
#!/bin/sh
i=10
echo $i
i=$[i+10]    # 结果为20
echo $i
i=$[i+100]    # 结果为120
echo $i
```

###4.expr命令
通过expr命令进行数学运算。注意，变量与运算符之间必须使用空格作为分隔符。
```
#!/bin/sh
i=10
echo $i
i=`expr $i + 10`    # 结果为20
echo $i
i=`expr $i + 100`    # 结果为120
echo $i
```

###5.bc命令
bc命令是一个支持精确的浮点运算的高级计算器，支持数学函数调用。它的功能很强大支持交互式与非交互式计算。
```
#!/bin/sh
i=10
echo $i
j=3;
echo $j
m=`expr $i / $j`   # 结果为3
echo $m
n=`echo "scale=9; $i / $j" | bc`    # 结果为3.333333333，scale=9保留小数点后9位
echo $n
```






