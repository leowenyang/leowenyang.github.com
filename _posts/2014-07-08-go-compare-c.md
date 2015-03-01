---
layout: post
title:  go 和 C 比较
category: go 
img: go.jpg
description : 比较go 和 c，方便go 语言的学习 
keywords: go c
---

## go 和 C 的语法比较

#### 常量

<table border="1">
    <tr>
        <th></th>
        <th>go 语言</th>
        <th>c  语言</th>
    </tr>
    <tr>
        <td>定义</td>
        <td>
            <pre>
            1. const PI float64 = 3.14
            2. const (
                PI float64 = 3.14
                True bool = true
                )
            3. 有类型
            </pre>
        </td>
        <td>
            <pre>
            1. #define PI 3.14
            2. 无类型
            </pre>
        </td>
   </tr>
   <tr>
    <td> 常用类型 </td>
    <td> 
        1. 字符常量
        2. 字符串常量
        3. 布尔类型常量
        4. 数值常量
    </td>
    <td> 只有宏定义，没有类型常量（C++中可以有和go一样的常量定义）</td>
   </tr>

</table>

#### 变量

<table border="1">
    <tr>
        <th></th>
        <th>go 语言</th>
        <th>c  语言</th>
    </tr>
    <tr>
        <td>定义</td>
        <td>
<pre>
1. var x string = "hello world"
2. x string = "hello world"
3. x := "hello world" -- 只能用在函数内部
</pre>
        </td>
        <td><pre>int x;</pre></td>
    </tr>

    <tr>
        <td>变量范围</td>
        <td>全局变量的范围是包，局部变量是函数</td>
        <td>全局变量的范围是整个程序，局部变量是函数</td>
   </tr>

    <tr>
        <td>类型转换</td>
        <td>强制类型转换只支持同类变量转换</td>
        <td>无限制</td>
   </tr>
</table>

#### 内置数据类型

#### 控制流程

#### 函数

#### 结构体

