在Bash中默认为字符串类型，其他类型我们可以通过declare来定义。
##1.字符串型
Bash中的默认数据类型。
```
string="hi my name is djangowang"   
echo $string
```
##2.数值型
在Bash中字符串类型只能用于字符串比较不能进行数学运算。我们通过declare -i来定义数值型。
```
declare -i number  # 定义一个数值型比那辆

```
我们来对比一下字符串型与数字型。
```
# 字符串
n=6/3
echo "n = $n"       # n = 6/3

# 数值型 
declare -i n
n=6/3
echo "n = $n"       # n = 2
```

##3.函数

##4.数组

##5.只读变量

##6.unset

declare -r var1
declare -i number
declare -f 函数 
declare -a 数组
