## 1. while循环语法

条件表达式:

```
while [ 条件表达式 ];do    # 推荐
    执行内容
done  

# 或

while [ 条件表达式 ]
do
    执行内容
done

# 或

while [ 条件表达式 ];do 执行内容 ；done    # Bash语句大都可以写作一行，只不过可读性差
```

命令方式:

```
while command;do
    执行内容
done
```

## 2.while循环案例

1.打印1-100的数。

```
#!/bin/bash
i=1
while [ $i -le  "100" ];do
   echo $i
   i=$((i+1))
done
```

2.打印1-100间的偶数。

```
#!/bin/bash
i=1
while [ $i -le  "100" ];do
   tmp=$((i%2))
   if [ $tmp -eq 0 ];then
       echo $i     
   fi
   i=$((i+1))
done
```

3.打印/etc/passwd信息。

```
#!/bin/bash    
while read line    # 推荐
do
    echo $line
done < /etc/passwd 

# 或

#!/bin/bash
cat /etc/passwd | while read line
do
    echo $line
done
```

4.死循环  
死循环中条件表达式永远为真，如果要退出死循环可以用ctrl+c方式.

```
#!/bin/bash
while true ;do
    echo "hello world"
done

# 或
while : ;done
    echo "hello world"
done
```

## 3.while循环中赋值的问题


