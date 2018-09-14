在Bash中默认为字符串类型，其他类型我们可以通过declare来定义。
##1.字符串型
Bash中的默认数据类型。
```
#!/bin/bash
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
#!/bin/bash
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
#!/bin/bash
declare -a array
array=(A B "C" D)
echo "第一个元素为: ${array[0]}"
echo "第二个元素为: ${array[1]}"
echo "第三个元素为: ${array[2]}"
echo "第四个元素为: ${array[3]}"

```
##4.显示函数
declare -f 显示函数
```
#!/bin/bash
function a(){
    echo "test1"
}

function b(){
    echo "test1"
}
declare -f    # 显示以上函数
declare -f a    # 限制指定函数
```

##5.设置环境变量
declare -x指定的变量会成为环境变量，可供shell以外的程序来使用。
```
#!/bin/bash
declare -x STRING="hello world"    # 定义一个string的环境变量,建议环境变量为大写
export -p    # 列出所有的shell赋予程序的环境变量
```

##6.只读变量
declare -r var1与readonly var1作用相同。当设置只读变量后，变量内容不可以修改
```
declare -r var1    # 设置一个只读变量
```
案例。
```
#!/bin/bash
myUrl="http://blog.puppeter.com/"
readonly myUrl
myUrl="http://blog.puppeter.com/"    # 当修改变量时会报错误“/bin/sh: NAME: This variable is read only.”
```

##6.unset变量
unset用于删除变量。他有两个参数-f（仅删除函数）-v(仅删除变量)默认值。 
```
#!/bin/bash
foo="hello world"
echo $foo    # 输出hello world
unset foo    # 删除foo变量
echo $foo    # 为空
```

