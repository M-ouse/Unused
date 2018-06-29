---
layout: post
title:  "Basic Grammar"
date:   2018-06-27
tags:
- Grammar
description: ''
categories:
- Learn Assemble Language
---

* MOV（传送）
指令写法：MOV  target，source

功能描述：将源操作数source的值复制到target中去，source值不变

注意事项：1）target不能是CS（代码段寄存器），我的理解是代码段不可写，只可读，所以相应这地方也不能对CS执行复制操作。2）target和source不能同时为内存数、段寄存器（CS\DS\ES\SS\FS\GS）3)不能将立即数传送给段寄存器4）target和source必须类型匹配，比如，要么都是字节，要么都是字或者都是双字等。4）由于立即数没有明确的类型，所以将立即数传送到target时，系统会自动将立即数零扩展到与target数的位数相同，再进行传送。有时，需要用BYTE PTR 、WORD PTR、 DWORD PTR明确指出立即数的位数

写法示例：MOV  dl,01H;MOV  eax,[bp]; eax =ss:[bp] 双字传送。

* LEA(装入有效地址)

指令写法：LEZ reg16，mem

功能描述：将有效地址MEM的值装入到16位的通用寄存器中。

写法示例：假定bx=5678H，EAX=1,EDX=2

>Lea si,2[bx]             ;si=567AH

>Lea di,2[eax][edx]       ;di=5

注意，这里装入的是有效地址，并不是实际的内存中的数值，如果要想取内存中该地址对应的数值，还需要加上段地址才行，而段地址有可能保存在DS中，也有可能保存在SS或者CS中哦:>不知道我的理解可正确。。。。