title: "Step into Groovy - 01 - 安装与运行"
date: 2015-04-16 08:02:48
categories: groovy
tags: groovy
toc: true
---

摘要

> goovyConsole

## Begin

### 简介

- Groovy 是一门动态语言。
- Groovy 语法和 Java 很相似，可以在代码中与 Java 互相调用，Groovy 实际上就是 Java。

### 与Java的区别

- 动态类型
- 脚本语言
- 允许省略每行的分号
- 默认限定符为 public
- 可以省略方法参数的括号
- 不必写 return 语句，会自动返回最后一句表达式的结果

### 安装Groovy

Mac环境下

```shell
brew install groovy
```

Windows环境下

1. 设置系统变量 `GROOVY_HOME=D:\Groovy-2.3.8`
2. PATH中添加 `%GROOVY_HOME%\bin`

### 第一个 Groovy 程序

#### 编译 Groovy 脚本

Groovy 脚本是解释型的，但是也可以进行编译型的。类似 Java，编译使用的是 groovyc 命令。groovy 和 groovyc 就类似 java 的 java 命令和 javac 命令。
编译后会产生标准的 java 的 *.class 文件，也可以通过 Java 命令进行运行。

#### 运行 Groovy 脚本

##### 在命令行中运行Groovy脚本

```shell
E:\blog\groovy>groovy -e "println 'hello world'"
hello world
```

-e 指定脚本内容

##### 运行本地Groovy脚本文件

新建一文件，命名为hello.groovy，添加内容为`println "Hello World"`
定位到该文件根目录

```shell
E:\blog\groovy>groovy hello.groovy
Hello World
```

##### 在GUI界面中运行Groovy脚本

在终端中输入`groovyConsole`会打开一个Groovy的GUI界面。整个界面分上下两块，上面是可输入的代码输入区，下半部会输出结果。

在输入区域输入`println "Hello World"`，然后选择Scipt-Run可以看到同样的结果

#### 编写 Groovy 类

建立文件"HelloWorld.groovy"，添加内容

```groovy
class HelloWorld {

    static void main(args) {
        println("Hello World")
    }
}
```

然后运行`groovy HelloWorld`

这里可以看到 groovy 类和 java 类非常相似，实际上 Groovy 就是 Java

再建一个文件"HelloWorld2.groovy"

```groovy
public class HelloWorld2 {

    public static void main(String[] args) {
        System.out.println("Hello World")
    }
}
```

然后运行`groovy HelloWorld2`，可以看到采用 Java的语法也能正常运行，只是代码更复杂


