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

## 4.小括号\(\)与 大括号{}

\(\)和{}都是对一串的命令进行执行，但有所区别：

* \(\)只是对一串命令重新开一个子shell进行执行 
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

### 通过${}避免变量混淆

```
#!/bin/bash
string="hello"
echo $string_aaa    # 不加${}情况，输出为空
echo ${string}_aaa    # 加${}情况，输出为hello_aaa
```

### 变量内部匹配

${ } 的一些特异功能：  
假设我们定义了一个变量为：  
file=/dir1/dir2/dir3/my.file.txt  
我们可以用 ${ } 分别替换获得不同的值：  
${file\#_/}：拿掉第一条 / 及其左边的字符串：dir1/dir2/dir3/my.file.txt  
${file\#\#_/}：拿掉最后一条 / 及其左边的字符串：my.file.txt  
${file\#_.}：拿掉第一个 . 及其左边的字符串：file.txt  
${file\#\#_.}：拿掉最后一个 . 及其左边的字符串：txt  
${file%/_}：拿掉最后条 / 及其右边的字符串：/dir1/dir2/dir3  
${file%%/_}：拿掉第一条 / 及其右边的字符串：\(空值\)  
${file%._}：拿掉最后一个 . 及其右边的字符串：/dir1/dir2/dir3/my.file  
${file%%._}：拿掉第一个 . 及其右边的字符串：/dir1/dir2/dir3/my

记忆的方法为：
是去掉左边\(在鉴盘上 \# 在 $ 之左边\)
% 是去掉右边\(在鉴盘上 % 在 $ 之右边\)  
单一符号是最小匹配﹔两个符号是最大匹配。  
${file:0:5}：提取最左边的 5 个字节：/dir1  
${file:5:5}：提取第 5 个字节右边的连续 5 个字节：/dir2  
我们也可以对变量值里的字符串作替换：  
${file/dir/path}：将第一个 dir 提换为 path：/path1/dir2/dir3/my.file.txt  
${file//dir/path}：将全部 dir 提换为 path：/path1/path2/path3/my

### 变量参数替换

变量的参数替换。

| 命令 | 解释 | 备注 |
| :--- | :--- | :--- |
| ${file-my.file.txt} | 若 $file 没设定,则使用 my.file.txt 作传回值 | 空值及非空值不作处理 |
| ${file:-my.file.txt} | 若 $file 没有设定或为空值,则使用 my.file.txt 作传回值 | 非空值时不作处理 |
| ${file+my.file.txt} | 若$file 设为空值或非空值,均使用my.file.txt作传回值 | 没设定时不作处理 |
| ${file:+my.file.txt} | 若 $file 为非空值,则使用 my.file.txt 作传回值 | 没设定及空值不作处理 |
| ${file=txt} | 若 $file 没设定,则回传 txt ,并将 $file 赋值为 txt | 空值及非空值不作处理 |
| ${file:=txt} | 若 $file 没设定或空值,则回传 txt ,将 $file 赋值为txt | 非空值时不作处理 |
| ${file?my.file.txt} | 若 $file 没设定,则将 my.file.txt 输出至 STDERR | 空值及非空值不作处理 |
| ${file:?my.file.txt} | 若 $file没设定或空值,则将my.file.txt输出至STDERR | 非空值时不作处理 |



