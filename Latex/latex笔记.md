# LaTeX笔记

链接：https://en.wikibooks.org/wiki/LaTeX

1.\newcommand命令：

https://blog.csdn.net/sinat_38816924/article/details/84349748

2.\DeclareMathOperator命令:

http://blog.sina.com.cn/s/blog_6f7b73770101kwzq.html

3.LaTeX优雅写出数学公式：

https://www.jianshu.com/p/f5d475d6904e

4.\makeatletter和\makeatother：

主要是因为latex @符号有参与相关的命令，使用\makeatletter可以使得之后的@成为普通的字母，再使用\makeatother又可以复原

https://www.douban.com/note/621707892/

5.\newtheoremstyle：

定义定理的风格是自己的风格：

```tex
\newtheoremstyle{stylename}% name of the style to be used
  {spaceabove}% measure of space to leave above the theorem. E.g.: 3pt
  {spacebelow}% measure of space to leave below the theorem. E.g.: 3pt
  {bodyfont}% name of font to use in the body of the theorem
  {indent}% measure of space to indent
  {headfont}% name of head font
  {headpunctuation}% punctuation between head and body
  {headspace}% space after theorem head; " " = normal interword space
  {headspec}% Manually specify head
```
https://en.wikibooks.org/wiki/LaTeX/Theorems
