## 1.函数语法
在Bash中函数有两种书写方式。
```
test(){    # 推荐书写方式
    函数内容
}

# 或


function test(){
    函数内容
}
```

## 2.函数案例
函数的案例。
```
#!/bin/bash
demo(){
    echo "this is my first function"
}
echo "-----函数开始执行-----"
demo
echo "-----函数执行完毕-----"
```

## 3.函数传入参数与返回参数
