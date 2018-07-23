---
layout: post
title:  "CTF_Re常见汇编语句"
date:   2018-06-27
tags:
- Grammar
description: ''
categories:
- Learning Assemble Language
---

* cmp    a,b     //  比较a与b  
* mov    a,b     //  把b值送给a值，使a=b  
* ret            //  返回主程序  
* nop            //  无作用，英文（no operation）简写，意思“do nothing”（机器码90） 
                          （ultraedit打开编辑exe文件看到90相当汇编语句的nop） 
* call           //  调用子程序，子程序以ret结尾  
* je或jz         //  相等则跳（机器码是74或84）  
* jne或jnz       //  不相等则跳（机器码是75或85） 
* jmp            //  无条件跳（机器码是EB） 
* jb             //  若小于则跳  
* ja             //  若大于则跳  
* jg             //  若大于则跳  
* jge            //  若大于等于则跳  
* jl             //  若小于则跳  
* pop xxx        //  xxx出栈  
* push xxx       //  xxx压栈  