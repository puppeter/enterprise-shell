在运行Shell时，会同时存在三种变量分别为局部变量、环境变量和内部变量。

## 1.局部变量

局部变量在脚本或命令中定义，仅在当前Shell实例中有效，其他Shell启动的程序不能访问局部变量。关于Shell变量：

* Shell脚本中定义的变量是global的，其作用域从被定义的地方开始，到shell结束或被显示删除的地方为止。
* Shell函数定义的变量默认是global的，其作用域从“函数被调用时执行变量定义的地方”开始，到shell结束或被显示删，函数定义的变量可以被显示定义成local的，其作用域局限于函数内。但请注意，函数的参数是local的。
* 如果同名，Shell函数定义的local变量会屏蔽脚本定义的global变量。

局部变量的关键字为"local",以下为局部变量案例。

```
#!/bin/bash
function Hello()
{
        local text="Hello World!!!"    #定义局部变量
        echo $text
}

Hello
echo $text    # 可以试着去掉函数中的local，再执行本脚本的效果
```

## 2.环境变量

所有的程序包括Shell启动的程序都能访问环境变量，有些程序需要环境变量来保证其正常运行。在Bash中可以通过以下三个命令来查看环境变量，他们区别在于:

* set 用来显示本地变量
* env 用来显示环境变量
* export -p 用来显示和设置环境变量

我们还可以通过以下两个文件来设置环境变量：

* /etc/profile
* ~./.bash\_profile

## 3.内部变量

Shell变量是由Shell程序设置的特殊变量。Shell变量中有一部分是环境变量，有一部分是局部变量，这些变量保证了Shell的正常运行。

| **内部变量** | **解释** |
| :--- | :--- |
| $BASH\_VERSION  |  bash版本 |
| $HOSTNAME| hostname |
| $HOME | 宿主目录（家目录） |
| $PATH | 环境变量 |
|  $RANDOM | 随机整数 |
  
  
  
  
  
  
 

