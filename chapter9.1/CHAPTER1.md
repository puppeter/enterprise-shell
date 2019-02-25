#sed 
sed被称为流编辑器，它是一种新型的非交互式的文本编辑器，它逐行处理文件或输入，并将结果输出到屏幕上。Sed编辑没有破坏性，它默认不会修改文件，除非使用选项主动修改。如果需要进行多项编辑任务，也可以把命令写在一个叫sed脚本的文件里。
## sed 语法
```
sed [-hnV][-e<script>][-f<script文件>][文本文件]
```
###参数说明
```
-e <script>或--expression=<script> 以选项中指定的script来处理输入的文本文件。
-f<script文件>或--file=<script文件> 以选项中指定的script文件来处理输入的文本文件。
-h或--help 显示帮助。
-n或--quiet或--silent 仅显示script处理后的结果。
-V或--version 显示版本信息。 
```

### 动作说明
```
a ：新增， a 的后面可以接字串，而这些字串会在新的一行出现(目前的下一行)～
c ：取代， c 的后面可以接字串，这些字串可以取代 n1,n2 之间的行！
d ：删除，因为是删除啊，所以 d 后面通常不接任何咚咚；
i ：插入， i 的后面可以接字串，而这些字串会在新的一行出现(目前的上一行)；
p ：打印，亦即将某个选择的数据印出。通常 p 会与参数 sed -n 一起运行～
s ：取代，可以直接进行取代的工作哩！通常这个 s 的动作可以搭配正规表示法！
```

### 案例
1.首先我们创建一个测试文件。
```
[root@blog.puppeter.com_centos ~]# cat /etc/passwd | head -n 10 | tee test
root:x:0:0:root:/root:/bin/bash
bin:x:1:1:bin:/bin:/sbin/nologin
daemon:x:2:2:daemon:/sbin:/sbin/nologin
adm:x:3:4:adm:/var/adm:/sbin/nologin
lp:x:4:7:lp:/var/spool/lpd:/sbin/nologin
sync:x:5:0:sync:/sbin:/bin/sync
shutdown:x:6:0:shutdown:/sbin:/sbin/shutdown
halt:x:7:0:halt:/sbin:/sbin/halt
mail:x:8:12:mail:/var/spool/mail:/sbin/nologin
operator:x:11:0:operator:/root:/sbin/nologin
```

2.在test文件的第4行追加blog.puppeter.com。
```
[root@blog.puppeter.com_centos ~]# sed -e "4a\blog.puppeter.com" test 
root:x:0:0:root:/root:/bin/bash
bin:x:1:1:bin:/bin:/sbin/nologin
daemon:x:2:2:daemon:/sbin:/sbin/nologin
adm:x:3:4:adm:/var/adm:/sbin/nologin
blog.puppeter.com
....
```

3.删除test文件的第5到第10行。
```
[root@blog.puppeter.com_centos ~]# sed '5,10d' test 
root:x:0:0:root:/root:/bin/bash
bin:x:1:1:bin:/bin:/sbin/nologin
daemon:x:2:2:daemon:/sbin:/sbin/nologin
adm:x:3:4:adm:/var/adm:/sbin/nologin
```

4.删除指定行号内容，譬如第一行。
```
[root@blog.puppeter.com_centos ~]# cat test  | sed '1d'
bin:x:1:1:bin:/bin:/sbin/nologin
daemon:x:2:2:daemon:/sbin:/sbin/nologin
...
```

5.删除3到最后一行
```
[root@blog.puppeter.com_centos ~]# cat test  | sed '3,$d'
root:x:0:0:root:/root:/bin/bash
bin:x:1:1:bin:/bin:/sbin/nologin
```

6. 





