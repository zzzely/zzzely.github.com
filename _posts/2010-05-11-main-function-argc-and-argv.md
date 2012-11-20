---
layout: post
title: main 函数中的argc和argv
date: 2010-05-11 22:29
comments: true
categories: [Coding]
tags: [main, argc, argv]
---
今天了解了下main函数中的这两个参数argc和argv。

通常c语言中main函数有以下三种形式

- int main()
- int main(int argc)
- int main(int argc,char *argv[])  此形式与 int main(int argc,char **argv)完全等同 

一般来说,上述三种形式中第一种和第三种比较常见,第二种很少使用,因为argc和argv这两个参数需要成对出现,只使用其中的一个参数没有意义.

这两个参数中 ,argc是一个整型变量,指的是命令行输入参数的个数,argv是字符串数组,它包含argc个字符串,每个字符串存储着一个命令行参数,如argv[0]存储着第一个命令行参数字符串,argv[1]存储着第二个命令行参数字符串,argv[argc-1]存储着最后一个命令行参数字符串.一般来说,argv[0]存储的是当前程序的路径与全称.
