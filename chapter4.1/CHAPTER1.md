正则表达式，又称规则表达式。（英语：Regular Expression，在代码中常简写为regex、regexp或RE），计算机科学的一个概念。正则表达式通常被用来检索、替换那些符合某个模式\(规则\)的文本。

[https://github.com/wzb56/13\_questions\_of\_shell/blob/master/15.regular-expression.md](https://github.com/wzb56/13_questions_of_shell/blob/master/15.regular-expression.md)


#基础的正则表示式
现在我们开始学习一些被称为元字符MetaCharacters的特殊字符。它们可以帮助我们创建更复杂的正则表达式搜索项。下面提到的是基本元字符的列表，

* `.` 点将匹配任意字符
* `[ ]`将匹配一个字符范围
* `[^ ]`将匹配除了括号中提到的那个之外的所有字符
* `*`将匹配零个或多个前面的项
* `+`将匹配一个或多个前面的项
* `?`将匹配零个或一个前面的项
* `{n}`将匹配 n 次前面的项
* `{n,}`将匹配 n 次或更多前面的项
* `{n,m}`将匹配在 n 和 m 次之间的项
* `{,m}`将匹配少于或等于 m 次的项
* `\`是一个转义字符，当我们需要在我们的搜索中包含一个元字符时使用

  


