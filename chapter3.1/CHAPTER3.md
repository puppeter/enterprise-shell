##1.for..in循环语法
for..in语法。
```
for 变量 in 条件语句；do    # 推荐
    执行语句
done

# 或

for 变量 in 条件语句
do
    执行语句
done 

# 或

for 变量 in 条件语句；do 执行语句 ；done 
```

##2.for..in循环语句
1.打印1-5的数字。

```
for loop in 1 2 3 4 5 ;do
    echo $loop
done 
```
2.打印1-100间的数字。
```
for loop in `seq 1 100`;do
    echo $loop
done 
```
3.创建1-100的文件夹。
```
for loop in `seq 1 100`;do
    mkdir $loop
done
```

