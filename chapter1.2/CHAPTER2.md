在Bash脚本语言中，变量的赋值方式共有四种分别是直接赋值、read赋值、命令赋值和位置参数赋值。

## 1.直接赋值

以下是一个Bash脚本,它将字符串“hi my name is djangowang”赋值给变量name并通过echo命令打印变量中的内容。

```
#!/bin/bash
name="hi my name is djangowang"   
echo $name
```

## 2.read命令赋值

read是Bash中的内建命令，它从键盘获取标准输出并赋值给变量。以下是将键盘输入的内容赋值给变量name,并通过echo命令打印变量中的内容。

```
#!/bin/bash
read name  
echo $name
```

## 3.命令赋值

获取系统命令的标准输出并将标准输出内容赋值给变量command，并通过echo命令打印变量中的内容。这里注意命令赋值方式共分为两种见以下案例。

    #!/bin/bash
    command = `date`    # 推荐赋值方式 ,其中“`” 是键盘按键1边上的符号。 
    echo $command

    # 或

    command = $(date)  
    echo $command

## 4.位置参数赋值

位置参数赋值是通过通过执行脚本时传递参数赋值给变量。譬如以下脚本名为test.sh内容如下，通过执行/bin/sh test.sh hello,其中hello就是位置参数他会通过$1赋值给command变量,这里注意如果位置变量有空格又需要同时传给位置变量1可以通过“”来扩起来，譬如/bin/sh test.sh "hello world"。这里位置变量通过空格作为变量的分割符。

```
#!/bin/bash
command = $1
echo $command
```

注意位置变量通常为数字$1-$9,10以上要用大括号扩起来如${10},${10},以下是案例。

```
#!/bin/bash
# argc.sh a b c d e f g h i j k
echo $1
echo $2
echo $3
echo $4
echo $5
echo $6
echo $7
echo $8
echo $9
echo ${10}
echo ${11}
```

以上程序有个问题，如果位置参数要是大于10或更多这样写程序成本会很高且程序易读性也不好，这时我们可以使用shift命令，它用于参数的自动左移。

```
#!/bin/bash
while [ $# != 0 ]
do
    echo "prama is $1,prama size is $#"
    shift
done
```



