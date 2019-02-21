# Bash版回收站
经常看到网上有人说把一个重要的文件删除了，而恢复成本很高，所以一直在想Linux终端中为什么没有像Windows下的回收站这样的设计，直到看到Unix编程艺术上的一段解释。 其实，Linux世袭了Unix的设计理念与传统，而Unix本身并没有这样的设计并延续到了Linux。 

Unix面向更加专业的用户 ,Unix的开发者喜欢清晰、简单的操作，用户告诉做什么就做什么，即便用户使用的命令等价于“向我开枪”的命令。而这样做Unix的开发本能辩解的就是：保护用户避免自我损害，应该是GUI或应用程序级别的事，而非操作系统:)。

这就解释了Linux终端为什么没有类似Windows回收站的设计，当然我们也可以通过Shell方式自己来实现一个类似回收站的功能，以下是笔者在2007年与2008年时写的shell回收站，供参考：
1.第一版本（http://bbs.chinaunix.net/thread-1034672-1-1.html） 
2. 第二版本http://m.blog.chinaunix.net/uid-7176662-id-2068124.html）


```
#!/bin/bash
#-----------------------------------------------------------------
#     filename:                                                                    
#       author: wds                                                                
#        begin:2008.1.27                                                                    
#          end:2008.2.1                                                                    
#      version: v.2       
# script address: http://blog.chinaunix.net/u1/40306/index.html
#-----------------------------------------------------------------
from1=$1
from2=$2
garbage=$HOME/.garbage
mvlog=$garbage/mv.log
if [ ! -e $garbage ]
then
    mkdir -p $garbage
    chmod 777 $garbage
fi
function rand
{
a=(0 1 2 3 4 5 6 7 8 9 a b c d e A B C D E F )
for ((i=0;i<7;i++));do
        echo -n ${a[$RANDOM % ${#a[*]}]}
done
}
random=$(rand)
function rm1
{
if [ -d "$from1" ]
then
   echo "rm: cannot remove '$from1/' : Is a directory"
else
   echo "`pwd`/:$from1:$random:`date`" >> $mvlog
   mv "$from1"  "$garbage/$from1:$random"
fi
}
function more
{
for file in *
do
echo "`pwd`/:$file:$random:`date`" >> $mvlog
mv $file "$garbage/$file:$random"
done 2> /dev/null
}
function rmi
{
if [ ! -d "$from2" ]
then
   echo -n "rm:remove regular empty file '$from2'?" ; read answer;
    if [ "$answer" = 'y' -o "$answer" = 'Y' ]
     then
        echo "`pwd`/:$from2:$random:`date`" >> $mvlog
         mv "$from2" "$garbage/$from2:$random"
    fi
else
   echo "rm: cannot remove directory '$from2': Is a directory"  
fi 

}
function rmf
{
if [ ! -d "$from2" ]
then
        echo "`pwd`/:$from2:$random:`date`" >> $mvlog
         mv "$from2" "$garbage/$from2:$random"
else
   echo "rm: cannot remove directory '$from2': Is a directory"
fi
}
function rmr
{
if [ -e "$from2" ]
then
        result=$(echo $from2 | sed 's/\///g')
        echo "`pwd`/:$result:$random:`date`" >> $mvlog
         mv "$result" "$garbage/$result:$random"
fi

}
function rml
{
while :
do
clear
line=$(cat -n $mvlog | awk -F : '{print $1,"FileName:"$2,    "Time:"$4}')
linecount=$(cat $mvlog | wc -l)
echo -e "$line\c"
echo 
echo 
echo "Please input number you want revent(line count:$linecount)--exit(e)"
read answer
if [ "$answer" = e -o "$answer" = E ]
  then
    break
else
    (
     echo "please input y(sure:)"
       read answer1
       if [ "$answer1" = y -o "$answer" = Y ]
        then
          address=$(sed -n "$answer""p" $mvlog | awk -F : '{print $1}')
          filename=$(sed -n "$answer""p" $mvlog | awk -F : '{print $2}')
          filerand=$(sed -n "$answer""p" $mvlog | awk -F : '{print $3}')
          fullname=$address$filename
           if [ -e "$fullname" ]
            then
               echo "The file exist!"
               sleep 1
           else
               old="$garbage/$filename:$filerand"
               new="$address$filename"
               mv "$old" "$new"
               delline=$( cat $mvlog | sed "$answer""d" | sort -o $mvlog)
               echo "update ok!!!"
               sleep 1
           fi
       fi
    )
  fi 
done

}
function help
{
    echo "
    -i)  If you wants delete some file , this function is confirm you want,the same as old rm.
    -f)  If you wants delete some directory ,you can use this function ,the same as old rm.
    -r)  If you wants delete some directory of file ,this function can use , the same as old rm.
    -l)  This is new function,is you wants resume some file or directory you can use this function,
         first this function can list some file in you garbage , these have some number ,if you 
         wants resume 1,you can input 1 and then input y to confirm.
    If you want add some function or some new idear please contact me...
         author:wds
          email:8851970@qq.com
    "
}

case "$1"
  in
[a-z]) : ;;
[0-9]) : ;;
[A-Z]) : ;;
    ?) more ;;
    *) :;;
esac
if [ "$#" -eq 0 ]
then
   echo -n "rm: missing operand
Try 'rm --help' for more informaction.
"
fi
if [ "$#" -eq 1 ]
then
   case "$from1" 
      in 
       -i) echo "Try 'rm --help' for more informaction."; break ;;
       -f) echo "Try 'rm --help' for more informaction."; break ;;
       -r) echo "Try 'rm --help' for more informaction."; break ;;
       
       -l) rml ;;
   --help) help;;
        *) rm1;;
   esac
fi

if [ "$#" -eq 2 ]
then
    case "$from1"
      in 
       -i) rmi ;;
       -f) rmf ;;
       -r) rmr ;;
       -l) rml ;;
      -rf) rmr ;;
   --help) help ;;
    esac
fi 

if [ "$#" -gt 2 ]
then
   for file in $*
     do
       mv $file "$home/"
   done 2> /dev/null
fi
```
