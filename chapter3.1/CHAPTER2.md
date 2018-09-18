##1.for语法
for语法。
```
for (( ; ; ))；do    # 推荐
    执行内容
done

# 或

for (( ; ;))
do
    执行内容
done

# 或
for ((;;));do 执行内容 ；done 
```

##2.for案例
1.打印1-100的数字。

```
for ((i=1; i<=100; i ++))
do
    echo $i
done
```
2.打印1-100间的奇数。
```
#!/bin/bash
for((i=1;i<=100;i++));do
   tmp=$((i%2))
   if [ $tmp -ne 0 ];then
       echo $i     
   fi
done
```
3.死循环。
死循环中条件表达式永远为真，如果要退出死循环可以用ctrl+c方式.
```
#!/bin/bash
for((;;));do
    echo "hello world"
done
```


