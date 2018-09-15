## 1. 调用系统命令符号 \`\` 与 $\(\)

在Linux中\`\`和$\(\)都是用来执行系统命令的符号。

    #!/bin/bash
    mem=`free -m`
    disk=$(df -h)

    echo $mem    
    echo $disk

在Linux中两个符号各有优缺点还要看用户的应用场景：

* \`\`基本上可用在全部的Shell版本中使用其移植性比较高，但反单引号容易打错或看错。
* $\(\)并不是所有shell都支持啊。

## 2. \转义与\续行

在Linux中“\”有两种含义分别为转义和换行。

* 转义，将Linux中的一些特殊符号转为本身含义。譬如在屏幕上打印command=`ls`，案例如下
      #!/bin/bash
      string="command=`ls`"    # 打印出ls执行结果
      string=command=\`ls\`    # 转义后的效果。
* 续行，通常用于Linux参数太长进行续行。以下案例为源码编译安装Nginx,因为一行装不下所有的参数，通常通过“\”进行续行
  ```
  ./configure --sbin-path=/usr/local/nginx/nginx \
  --conf-path=/usr/local/nginx/nginx.conf \
  --pid-path=/usr/local/nginx/nginx.pid \
  --with-http_ssl_module \
  --with-pcre=/usr/local/src/pcre-8.21 \
  --with-zlib=/usr/local/src/zlib-1.2.8 \
  --with-openssl=/usr/local/src/openssl-1.0.1c
  ```

## 3.单引号和双引号

在Bash环境下单引号和双引号是有区别的，这很像PHP语言。

* 双引号，解析双引号内部的特殊符号
* 单引号，不解析单引号内部的内容

  ```
  #!/bin/bash
  echo "hello\tworld"    # 双引号，打印结果为hello    world ，双引号会解析内部的特殊符号。
  echo 'hello\tworld'    # 单引号，打印结果为hello\tworld，不转义\t特殊符号
  ```
  
如果双引号中有多个特殊符号，我只想部分不转义怎么办？譬如以下案例不转义\n，可以在双引号中使用"\"不转义
```
#!/bin/bash
echo "hello\tworld\\n"    # 最终打印结果为hello    world\n
```



## 4.小括号()与 大括号{}

()和{}都是对一串的命令进行执行，但有所区别：

* ()只是对一串命令重新开一个子shell进行执行 
* {}对一串命令在当前shell执行,

案例1，在Linux和Shell中可以通过{}把一组命令一起执行，不过这里有两种方式在大括号中执行系统命令，分别用,和..进行分割。譬如我要创建a.txt、b.txt和c.txt文本文件。
```
touch {a,b,c}.txt    # 用,进行分割方式
touch {a..c}.txt    # 用..进行分割方式
```
案例2，在Linux和Shell中可以通过{}把一组命令一起执行，不过这里有两种方式在大括号中执行系统命令，分别用,和..进行分割。譬如我要创建a.txt、b.txt和c.txt文本文件。
```
(ls && touch {a..f} && ls )    # 将多个命令放到（）中，用子Shell方式运行。 && 表示前一个命令执行成功的情况下再执行后一个命令
```



## 5.大括号${} 
${}可以存放变量与"$"符号的变量相比，他主要用于避免变量的混淆，譬如以下案例。
```
#!/bin/bash
string="hello"
echo $string_aaa    # 不加${}情况，输出为空
echo ${string}_aaa    # 加${}情况，输出为hello_aaa
```






## echo 与特殊字符

特殊符号对照表，表1。

| 符号 | 含义 |
| :--- | :--- |
| \n | 新行 |
| \r | 回车 |
| \t | 制表符 |
| \v | 垂直的制表符 |
| \b | 后退符 |
| \a | 警告（蜂鸣或是闪动） |

