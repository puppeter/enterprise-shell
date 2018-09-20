select 是个无限循环，因此要记住用break命令退出循环或用exit命令终止脚本。也可以按ctrl+c 退出循环。

##1.select循环语法

```
select name   [in   list ];do    # 推荐 
    执行语句
done

# 或

select name   [in   list ] 
do 
    执行语句
done
```


##2.select循环语句案例
通常我们使用select用来做列表，案例如下：
```
#!/bin/bash
echo "What is your favourite OS?"
select var in "Linux" "Windows" "Free BSD" "Other"; do
    break;
done
echo "You have selected $var"
```