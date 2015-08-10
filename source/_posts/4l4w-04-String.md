title: "4l4w - 04.String"
date: 2015-08-10 08:05:53
tags: [Java, Groovy, Scala, Kotlin]
categories: 4l4w
toc: true
---

# String

## Java

### 声明字面量

```java
String s = "Hello World";
```

### 遍历字符

```java
for (char c : s.toCharArray()) {
    System.out.println(c);
}
```

### 多行文本

```java
String text =
        "\t1, 2, 3\n" +
                "\tone, two, three\n" +
                "\t\"x\", \"y\", \"z\"";
```

在 Java 中表示多行文本和特殊字符时需要使用对应的转义符，看起来很不直观

### 模板 Template

所谓的模板就是使用变量或表达式来代替字符串中通过特殊符号包裹的子串。

Java 并没有字符串模板，要想实现模板功能只有自己解析字符串，使用 `replace()` 等方法来进行模拟。

```java
String name = "Peter";
String str = "name=$name, ${name.length()}";
System.out.println(
        str.replace("$name", name)
                .replace("${name.length}", "" + name.length()))；
```

以上的例子中使用了变量 `name` 的值来代替字符串中的 `$name` 子串。

### 常用方法

```java
//获取某一位置的字符
System.out.println(s.charAt(2));    //  l

//截取子串
System.out.println(s.substring(6, 9));  //  Wor
```

## Groovy

### 声明字面量

```groovy
def s = "Hello World"
```

### 遍历字符

```groovy
for (c in s) {
    println(c)
}
```

### 多行文本

```groovy
def text =
"""    1, 2, 3
one, two, three
"x, "y", "z\""""
```

Groovy 中可以使用三个双引号表示原样输出，在三个双引号之间可以任意换行，使用特殊字符，可以看到这种设计比起 Java 来说要直观，简单很多。

但是需要注意的是如果要输出的字符串结尾也是双引号，则必须像以上例子一样在最后一个双引号前加上转义符 "\"，否则编译器会将此双引号和三个双引号看做是两组双引号而报编译错误。

### 模板 Template

```groovy
def name = "Peter"
def str = "name=${name}, ${if (name.length() > 10) 10 else name.length()}";
println(str)    //  name=Peter, 5
```

Groovy 中可以使用 `${}` 来实现字符串模板，大括号之间的字符会被解析为代码，代码的结果会被当做字符串来输出，看起来就像是使用 Javascript 的 `eval` 函数一样，比起 Java 来说方便许多，再也不用使用一堆加号连接字符串和变量了。

### GString

实际 Groovy 中可以使用单引号和双引号来表示字符串，大部分情况下这两者都是一样的用法。但是使用上述模板时必须使用双引号，因为使用引用符号 `${}` 的双引号字符串会被解析为 Groovy 内置的字符串类 GString。该类是 String 类的补充，拥有很多特殊的方法。而单引号字符串或不包含引用符号的字符串都会被解析为普通的 String 类。

### 常用方法

```groovy
//获取某一位置的字符
println(s[2])   //  l

//截取字符串，"<" 表示不包含
println(s[6..9])    //  Worl
println(s[6..<9])   //  Wor

//返回从字符串中减去某一部分的新字符串
println(s - "l" - "World")  //  Helo
```

## Scala

### 声明字面量

```scala
val s = "Hello World"
```

### 遍历字符

```scala
for (c <- s) {
  println(c)
}
```

### 多行文本

```scala
val text =
  """  1, 2, 3
one, two, three
"x, "y", "z""""
```

### 模板 Template

Scala 的字符串模板主要依赖于两种插值器（Interpolator）：s 插值器和 f 插值器

s 插值器

s 插值器主要用于进行简单的字符串替换，声明时直接使用字符 "s"连接字符串且当中不要有空格。

```scala
val name = "Peter"
val str = s"name=$name, ${if (name.length() > 10) 10 else name.length}"
println(str)  //  name=Peter, 5
```

f 插值器

f 插值器主要用于进行格式化输出，类似 `String.format()` 的功能。

```scala
val salary = 100.1
println(f"$name%s has $salary%.5f") //  Peter has 100.10000
```

### 常用方法

```scala
println(s.charAt(2))  //  l
println(s.substring(6,9)) //  Wor
```

## Kotlin

### 声明字面量

```kotlin
val s = "Hello World"
```

### 遍历字符

```kotlin
for (c in s) {
    println(c)
}
```

### 多行文本

```kotlin
val text =
"""     1, 2, 3
    one, two, three
    "x, "y", "z""""
```

### 模板 Template

```kotlin
val name = "Peter";
val str = "name=${name}, ${if (name.length() > 10) 10 else name.length()}";
println(str)    //  name=Peter, 5
```

### 常用方法

```kotlin
println(s[2])
println(s.substring(5, 8))
```

