---
title: 编译原理知识点小总结
date: 2018-03-11 12:00:00
categories: 技术贴 | 总结类
tags: summary
thumbnail: https://pub.wangxuefeng.com.cn/asset/blogthumbnail/Summaryofcompilingprinciple/thumbnail.png
---

# 编译原理基础知识 Q & A

## Q1.有哪些编程语言是编译执行的，哪些是解释执行的？

- 编译执行：

>```C```、```C++```、```Pascal/Object Pascal（Delphi）```等

- 解释执行：

>```JavaScript```、```VBScript```、```Perl```、```Python```、```Ruby```、```MATLAB```、```PHP```、```ASP```、```解释性Basic语言```等

- 先编译后解释:

>```Java```、```JSP```、```C#```等

## Q2.编译器的概念？

> A compiler is a program that reads a program written in a source language and translates it into an equivalent program in a target language.

> 编译器是一个读取用源语言（高级语言，接近自然语言）编写的程序并将其转换成与之等价的目标语言（低级语言，汇编语言和机器语言）的程序。

## Q3.编译器的合作伙伴有哪些？各完成什么功能？

- 1.预处理器:在真正的编译开始之前由编译器调用的独立程序。预处理器可以删除注释、包含其他文件以及执行宏替代(宏定义)

- 2.汇编器：将汇编语言翻译为机器语言的程序

- 3.链接加载编辑器：将机器语言关联目标机并转化成可执行程序，然后将可执行程序加载到内存并进行执行

## Q4.编译器逻辑上包含哪几个阶段？分析和综合阶段、前端和后端都各包含哪些阶段？

- 分析阶段（前端）： 词法分析，语法分析，语义分析，中间代码生成

- 综合阶段（后端）： 代码优化，目标代码生成

- 辅助阶段（贯穿始终）： 符号表管理，错误处理

![逻辑阶段](https://pub.wangxuefeng.com.cn/asset/blogthumbnail/Summaryofcompilingprinciple/ljjd.jpg)

## Q5.自己遇到的词法、语法、语义错误有哪些？

- 词法错误：

	- 1.赋值符"="与比较符号"=="混淆，常在条件语句中出错，如

		```C
			if(i = 10){
				//do something
			}else{
				//do something
			}
		```			
	像以上这样的写法，错误不容易发现，而且在部分语言中程序还会照常执行，因此可使用以下写法

		```C
			if(10 == i){
				//do something
			}
		```	
	将常量写在前，变量写在后，若无意将比较符号"=="写为类赋值符"="，程序将会报错警告

	- 2.&和|不同于&&和||，	&和|是按位与和或，&&和||是逻辑运算符（与和或）

	- 3.字符与字符串混淆

		> 单引号包起来的字符事实上是一个整数，整数值对应于该字符在编译器采用的字符集的序列值。如'a'与0141（八进制）97（十进制）完全一致。

		> 双引号引起来的字符串代表一个指向无名数组的起始字符的指针。该数组被双引号之间的字符以及一个'\0'初始化。

- 语法错误：

	- 1.变量标识符定义错误，如

		```c
			int 1i; 
			//变量标识符不能以数字开头
		```

	- 2.保留关键字单词出错或者使用保留关键字作变量，如

		```c
			chat a;			//应该是 char a;
			int long = 1;	//long是保留关键字
		```

	- 3.配对符号不匹配，如

		```c
			float a = 1.0;
			float b = 2.0;
			float c = a * ( b + a / b;  //缺少右括号
		```


- 语义错误：

	- 1.变量未定义，如

		```c	
			int a = 1;
			int c = a + b; //b未定义
		```	

	- 2.函数实参形参类型不兼容,或返回值类型不兼容，如	

		```c		
			int add(int a, int b){
				return  a+ b;
			}
			double a = 3.14;
			double b = 2.96;
			double res = add(a,b);
			// double类型不能自转为int类型，参数及返回值的类型都不兼容
		```



## Q6.长度为n的字符串的（真）前缀、后缀、子串、子序列各有多少个？（假设字符串中不存在相同字符）

- 前缀: n＋1 个

	>前缀分别是ε、只含第一个字符的子串、只含前两个字符的子串、只含前3个字符的子串、……、含前n个字符的子串

- 后缀: n＋1 个

	>后缀分别是ε、只含最后一个字符的子串、只含最后两个字符的子串、只含最后3个字符的子串、……、含最后n个字符的子串

- 子串: ![n(n+1)/2](https://pub.wangxuefeng.com.cn/asset/blogthumbnail/Summaryofcompilingprinciple/nD2.jpg)+1个

	>长度为0的子串1个，长度为1的子串n个，长度为2的子串n－1个，长度为3的子串n－2个，……，长度为n－1的子串2个，长度为n的子串1个

- 真前缀: n-1 个
	
	>真前缀比前缀少了一个串本身和ε

- 真后缀: n-1 个

	>真后缀也比后缀少了一个串本身和ε

- 子序列: 2<sup>n</sup>个