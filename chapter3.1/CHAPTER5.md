until 循环执行一系列命令直至条件为 true 时停止。until 循环与 while 循环在处理方式上刚好相反，一般while循环优于until循环，但在某些时候，也只是极少数情况下，until 循环更加有用。

## 1.until循环语法
```
until command
do
   执行语句
done
```

## 2.until循环案例

```
#!/bin/bash
a=0
until [ ! $a -lt 10 ]
do
   echo $a
   a=`expr $a + 1`
done
```