title: "Step-into-Groovy-02-数据类型与作用域"
date: 2015-04-19 09:16:29
categories: groovy
tags: groovy
toc: true
---

摘要

> times()，upto()，downto()，step()，GString，类型转换，类型推断，作用域



## 数据类型与作用域

### 一切皆对象

Groovy 中一切皆对象，这意味着 Groovy 中不存在基本类型。

```groovy
int i = 1
def j = 2
println i.class	//class java.lang.Integer
println j.class	//class java.lang.Integer
```

可以看到在 Groovy 中基本类型实际是通过包装类实现的。

### 数据类型

#### 数字类型

常用方法

- `n.times{}`	*执行 n 次*
- `n.upto(m){}`	*执行 m-n+1 次*
- `n.downto(m){}`	*执行 n-m+1 次*
- `n.step(a,b){}`	*执行 (a-n)b 次，即从 n 开始，每次步长 b，直到等于 a*

```groovy
def store = ""
10.times { store += "x" }
assert store == "xxxxxxxxxx"

store = ""
1.upto(5) { n -> store += n }
assert store == "12345"

store = ""
2.downto(-2) { n -> store += n + "" }
assert store == "210-1-2"

store = ""
0.step(0.5, 0.1) { n -> store += n + "," }
assert store == "0,0.1,0.2,0.3,0.4,"
```

>A:

>可以用来代替 for 循环


#### 字符串

##### 概述

Groovy 中可以使用 Java 的 String 和 Groovy 的 GString 表示字符串。

原则

- 当没有明确指明类型时，字符串都会被推断为 String 类型
- String 可以用单引号或双引号声明，但是 GString 只能以双引号声明
- 只有 GString 支持使用引用符 `${}`
- 三引号 `"""` 或 `'''` 可以定义跨行的字符串，即按格式原样输出
- 双引号内部可以使用单引号，单引号内部可以使用双引号

```groovy
def x = 2
def singleQuote = 'abc'
def doubleQuotes = "abc"
def singleQuote2 = 'abc${x}'
def doubleQuotes2 = "abc${x}"
println singleQuote.class   //class java.lang.String
println doubleQuotes.class  //class java.lang.String
println singleQuote2.class  //class java.lang.String
println doubleQuotes2.class //class org.codehaus.groovy.runtime.GStringImpl

println singleQuote2        //abc${x}
println doubleQuotes2       //abc2
```

>A:

>尽量使用 GString 进行字符串拼接

##### 常用方法

```groovy
def str = 'Groovy&Grails&lxt008'
println str[4]                  //v
println str[-1]                 //8
println str[1..2]               //ro
println str[1..<3]              //ro
println str[4, 1, 6]            //vr&
println 'a' == 'a'              //true
println 'a' <=> 'a'             //0
println 'a'.compareTo('a')      //0
println 'a' - 'a'               //
println 'a' + 'a'               //aa
println 'a' * 3                 //aaa

str = 'Groovy'
println str.center(11)          //  Groovy
println str.center(2)           //Groovy
println str.center(11, '=')     //==Groovy===
println str.count('o')          //2
println str.leftShift(' world') //Groovy world
println str << ' world'         //Groovy world
println str.minus('vy')         //Groo
println str - 'vy'              //Groo

println str.next()              //Groovz
println str.previous()          //Groovx

println str.padLeft(4)          //Groovy
println str.padLeft(11)         //     Groovy
println str.padLeft(11, "=")    //=====Groovy

println str.replaceAll('[a-z]') { ch -> ch.toUpperCase() }  //GROOVY
println '123'.toDouble()                                    //123.0
println '123'.toList()                                      //[1, 2, 3]

//tokenize 返回 List，split 返回数组
str = "Groovy Grails&lxt"
println str.tokenize()                                      //[Groovy, Grails&lxt]
println str.tokenize('&')                                   //[Groovy Grails, lxt]
println str.tokenize().getClass().getName()                 //java.util.ArrayList
println str.tokenize("t").getClass().getName()              //java.util.ArrayList
println str.split("t").getClass().getName()                 //[Ljava.lang.String;
```

A：
```
使用 toDouble()等进行类型转换
```

### 类型推断

在 Java 中以下代码代表一个 String

```java
String value = "Hello World";
```

但是实际上从 "=" 右边就可以推断出这是一个 String，左边的类型声明有点多此一举。所以 Groovy 允许使用 def 定义变量，具体类型由 Groovy 根据右边的值进行推断。如果 Groovy 无法推断具体的类型则会把它当做是 Object。

```groovy
def value = "Hello World"
```

可以通过调用 `.class` 来查看变量的具体类型

```groovy
println value.class
```

因为 Groovy 是无类型的，所以方法中的参数也可以 **省略 def 关键字**

>A:

>除非必要，使用 def 定义变量


### 动态类型与静态类型

Groovy 支持动态类型和静态类型

动态类型

```groovy
def dynamicDate = new Date()
```

静态类型

```groovy
Date staticDate = new Date()
```

如果声明了静态类型，就不能再改变该变量的类型

## 作用域

###  Groovy 类
Groovy 类作用域同 Java

### Groovy 脚本

绑定域：脚本内的全局作用域，相当于该脚本对象的成员变量。如果没有定义过变量(可以直接使用或仅仅初始化但未声明)，其作用域即是绑定域。
本地域：脚本内的代码块。如果是定义过的变量，其作用域就是本地域。

脚本中声明的方法访问不了本地域

```groovy
String hello = "hello"	//定义变量，作用域是本地域
def world = "world"		//定义变量，作用域是本地域

helloworld = "hello world"	//全局变量，作用域是绑定域

void check() {
	println hello
    println world
    println helloworld
}
check()
```

