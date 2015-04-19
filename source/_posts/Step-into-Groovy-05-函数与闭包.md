title: "Step-into-Groovy-05-函数与闭包"
date: 2015-04-19 09:42:21
categories: groovy
tags: groovy
toc: true
---

摘要

>定义方法，参数默认值，返回值，定义闭包，方法与闭包区别


## 方法 函数 闭包

### 方法

#### 定义方法

在 Groovy 中定义方法的参数时无需指定参数类型。

```groovy
def say(name){
  println name
}
```

指定参数的默认值

```groovy
def say(name, word = "Hello ") {
  println word + name
}

say("Jack")                 //Hello Jack
say("Mary", "Good bye ")    //Good bye Mary
```

>A：
使用参数默认值来代替方法重载

#### 返回值

Groovy 总是会自动返回方法最后一个表达式的值，无需手动调用 return 语句。

```groovy
def add(x, y) {
  x += x
  y += y
  x + y
}

assert 16 == add(3, 5)
```

>A：
只在必要时显示使用 return 语句

### 函数字面值

#### 概述

- 函数字面值的定义和使用都近似方法，但是其可以被赋值给变量，从而可以被传递和执行
- 定义了一个函数字面值又被称为定义了一个闭包，从形式上看是由`{}`包围的代码块，是一个可执行的代码块
- 闭包实际是一个匿名内部类的对象
- 闭包可以嵌套，方法不能嵌套

#### 定义一个闭包

与方法不同，没有表示参数的括号，而多了等号

```groovy
def excite = { word ->
  return "${word}!!"
}
```

#### 使用默认参数

```groovy
def d = {name, address = 'Shanghai'->}
```

#### 调用闭包

```groovy
assert "Groovy!!" == excite("Groovy")
assert "Java!!" == excite.call("Java")
```

#### it

`it` 表示闭包内部的单个参数，所以定义闭包时如果只有单个参数，可以按如下方式简写

```groovy
def learn = {
  it
}
assert "Groovy" == learn("Groovy")
```

>A:
>
>使用 it 来表示单个参数

