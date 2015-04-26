title: "Step-into-Groovy-03-脚本"
date: 2015-04-19 09:24:08
categories: groovy
tags: groovy
toc: true
---

摘要

>运行脚本，绑定域


## 脚本

### 运行脚本

从命令行中运行指定脚本

```java
groovy example.groovy
```

在其它程序中运行指定脚本

```java
//有一脚本文件 example.groovy
def s = new example()
s.run()
```

也可以通过该脚本对象直接运行脚本内的函数

### 绑定变量

通过 new 建立的脚本对象可以绑定指定的值到该脚本的绑定域中

```java
//file: example.groovy
//绑定域
helloworld = "hello world"

def hello(){
  println(helloworld)
}

//file: other.groovy
def s = new example()
s.binding.goodbye = "good bye"	//绑定不存在的变量不会报错
s.binding.helloworld = "hello groovy"
s.hello()	//hello groovy
```

