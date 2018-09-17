## 1.文件测试符
文件测试符主要用于检测Linux/UNIX中的文件属性，以下是一些常见的文件测试符：
* -f:测试其是否为普通文件，即使用ls -l命令查看时，文件类型显示为-的文件；
* -d:测试其是否为目录文件，即使用ls -l命令查看时，文件类型显示为d的文件；
* -e:测试文件是否存在，不论是目录还是文件，如果存在则为真，否则为假；
* -r：测试文件对当前访问者来说（非创建者）是否可读；
* -w：测试文件对当前访问者来说（非创建者）是否可写；
* -x：测试文件对当前访问者来说（非创建者）是否可执行；
* -s:测试文件是否有大小是否为0，如果不为0结果为真，否则为假；
* -l:测试文件是否为链接文件
* \! 取反

文件测试符案例。
```
#!/bin/bash

if [ -f /etc/passwd ];then    # 测试是否为普通文件
    echo "is file"
fi

if [ -d /etc/ ];then    # 测试是否为目录
    echo "is dirctory"
fi

if [ -e /etc/passwd ];then    # 测试文件是否存在
    echo "fie exists"
fi

if [ -r /etc/passwd ];then    # 测试是否可读
    echo "read ok"
fi

if [ -w /var/log/messages ];then    # 测试是否可写
    echo "write ok"
fi

if [ -x /var/log/messages ];then    # 测试是否可执行
    echo "execute ok"
fi

if [ -s /var/log/messages ];then    # 测试是否可执行
    echo "file lenght not zero"
fi

if [ -l /var/log/messages ];then    # 测试是否为链接文件
    echo "it's symbolic file"
fi

if [ ! -d /etc/passwd ];then    # 如果这不是一个目录结果为真
    echo "it's not  dirctory"
fi

[ ! -d /etc/djangowang ] && mkdir /etc/djangowang    # 如果目录不存在，就创建一个目录
```

##2.特殊符号的应用
当我们在使用if..else时，表达式为真的情况程序不做任何事时，这里可以通过":"来做相占位符号否则程序会报错，当表达式为假的情况时打印信息，案例如下。
```
#!/bin/bash
if [ -e "/etc/passwd" ];then
   :    # 占位符
else
   echo "file not exists"
fi
```