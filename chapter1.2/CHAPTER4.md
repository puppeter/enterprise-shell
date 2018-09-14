在运行Shell时，会同时存在三种变量分别为局部变量、环境变量和内部变量。
##1.局部变量
局部变量在脚本或命令中定义，仅在当前Shell实例中有效，其他Shell启动的程序不能访问局部变量。
```
#!/bin/bash
function Hello()
{
        local text="Hello World!!!"    #局部变量
        echo $text
}

Hello
```

##2.环境变量

##3.内部变量
