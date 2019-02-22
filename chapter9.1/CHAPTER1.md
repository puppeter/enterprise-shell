 #sed 

sed被称为流编辑器，它是一种新型的非交互式的文本编辑器，它逐行处理文件或输入，并将结果输出到屏幕上。Sed编辑没有破坏性，它默认不会修改文件，除非使用选项主动修改。如果需要进行多项编辑任务，也可以把命令写在一个叫sed脚本的文件里。


参数说明
* -e<script>或--expression=<script> 以选项中指定的script来处理输入的文本文件。
* -f<script文件>或--file=<script文件> 以选项中指定的script文件来处理输入的文本文件。
* -h或--help 显示帮助。
* -n或--quiet或--silent 仅显示script处理后的结果。
* -V或--version 显示版本信息。