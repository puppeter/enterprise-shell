## 函数语法与案例
在编程中，为了简化代码量，通常会将经常调用的一些代码模块化，并一一个名字表示，当再次使用该模块时只需要输入该名字，系统会自动去读取该名字所对应的代码模块。因此在计算机中把一段独立功能的代码当做一个整体，并为之命一个名字，命名的代码段即为函数。

## 1.函数语法
在Bash中函数有两种书写方式。
```
functionName(){    # 推荐书写方式
    函数内容
}

# 或

function functionName(){
    函数内容
}
```

## 2.函数案例
1.函数的调用。
```
#!/bin/bash
demo(){
    echo "this is my first function"
}
demo
```

2.函数的参数传递。
```
#!/bin/bash

test(){
    echo $1
    echo $2
}
test "hi" "where do you come from"
```

3.函数的返回
在Bash中函数通过return内建命令返回(注：return只能返回数值型)。
```
#!/bin/bash
test(){

    if (( $1 > 10 ));then
        return 0
    else
        return 1    # 假如将return改为exit 0结果又会怎样
    fi
}

test "4"
echo $?
echo "end.."
```



