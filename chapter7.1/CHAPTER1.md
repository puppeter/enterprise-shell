#Bash脚本风格

Bash脚本要以
```
help()
{
cat << HELP
Usage:./test.sh [name]
this script is to print name
    h,--help   display this help and exit

HELP
exit 1
}
[ "$1" = "h" -o "$1" = "--help" -o ! $# -eq 1 ] && help
```