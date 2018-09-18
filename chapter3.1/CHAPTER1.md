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

1.打印1-100的数字。
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

## 3.while循环中赋值的陷阱
是否遇到过while循环内赋值的变量，在循环体外获取不到值得情况？下文案例来自http://www.cnblogs.com/f-ck-need-u/p/7431578.html。
while循环外获取不到值得情况。
```
#!/bin/bash
echo "abc xyz" | while read line
do
    new_var=$line
done
echo new_var is null: $new_var?    # 打印结果new_var is null:? ,new_var变量为空
```
while循环外可以获取到值。
```
#!/bin/bash
while read line
do
    new_var=$line
done <<< "abc xyz"
echo new_var is null: $new_var?    # 打印结果new_var is null:abc xyz? ,new_var变量为abc xyz
```
原因：因为使用到了“|”管道，所以while语句在子Shell中执行，这意味着while语句内部设置的变量、数组、函数等在循环外部都不再生效。“<<<”以这种方式直接在命令之前分配的变量仅对命令进程生效。