---
layout: post
title: "linux/shell/eval command how to"
date: 2016-05-13 14:13:07 +0800
comments: true
categories: linux shell
---
1. eval command-line
其中command－line是在终端上键入的一条普通命令行。然而当在它前面放上eval时，其结果是shell在执行命令行之前扫描它两次。如：
pipe="|"
eval ls $pipe wc -l
shell第1次扫描命令行时，它替换出pipe的值｜，接着eval使它再次扫描命令行，这时shell把｜作为管道符号了。
如果变量中包含任何需要shell直接在命令行中看到的字符（不是替换的结果），就可以使用eval。命令行结束符（； ｜ &），I／o重定向符（< >）和引号就属于对shell具有特殊意义的符号，必须直接出现在命令行中。
2. eval echo \$$# 取得最后一个参数
如：cat last
eval echo \$$#
./last one two three four
four
第一遍扫描后，shell把反斜杠去掉了。当shell再次扫描该行时，它替换了$4的值，并执行echo命令
3.以下示意如何用eval命令创建指向变量的“指针”：
x=100
ptrx=x
eval echo \$$ptrx 指向ptrx，用这里的方法可以理解b中的例子
100 打印100
eval $ptrx=50 将50存到ptrx指向的变量中。
echo $x
50 打印50