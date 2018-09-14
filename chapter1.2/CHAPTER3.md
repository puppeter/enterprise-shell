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
declare -i number    # 定义一个数值型

```
我们来对比一下字符串型与数字型。
```
# 字符串
n=6/3
echo "n = $n"    # n = 6/3

# 数值型 
declare -i n
n=6/3
echo "n = $n"    # n = 2
```

##3.数组
数组中可以存放多个值。Bash只支持一维数组，不支持多维数组，初始化时不需要定义数组大小，与大部分编程语言类似数组元素的下标由0开始。
```
declare -a array    #

```
数组案例。
```
declare -a array
array=(A B "C" D)
echo "第一个元素为: ${array[0]}"
echo "第二个元素为: ${array[1]}"
echo "第三个元素为: ${array[2]}"
echo "第四个元素为: ${array[3]}"

```
##4.函数



##5.只读变量
```
declare -r var1    # 设置一个只读变量
```

##6.unset

declare -r var1
declare -i number
declare -f 函数 
declare -a 数组
