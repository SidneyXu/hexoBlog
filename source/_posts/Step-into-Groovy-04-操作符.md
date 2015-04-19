title: "Step-into-Groovy-04-操作符"
date: 2015-04-19 09:40:21
categories: groovy
tags: groovy
toc: true
---

摘要

>相等，安全引用操作符，猫王操作符

## 操作符

### 概述

Groovy 中的操作符实际都是方法，且支持操作符的重载

### 相等

遵循最小意外原则，Groovy 中 `==` 等于 Java 中的 `equals()` 方法。要检查是否对象相等，需使用 `is()` 函数

```groovy
Integer x = new Integer(2)
Integer y = new Integer(2)
Integer z

println x == y      //true
println x.is(y)     //false
println z == null   //true
println z.is(null)  //true
```

### 重载的操作符

```groovy
assert 4 + 3 == 7    			//4.plus(3)
assert 4 - 3 == 1    			//4.minus(3)
assert 4**3 == 64    			//4.power(3)
assert 4 / 3 == 1.3333333333	 //4.div(3)
assert 4.intdiv(3) == 1			//整除
assert 4 > 3   					//4.compareTo(3)
assert 4 <=> 3 == 1    			//4.compareTo(3)
```

### 安全引用操作符

`?.` 表示如果对象为空，则什么都不做

```groovy
//old
List<Person> people = [null, new Person(name: "Jack")]
for (Person person : people) {
  if (person != null) {
      println person.name
  }
}
//output
//Jack
println()

//new
for (Person person : people) {
  println person?.name
}
//output	 仍然会被输出，仅表示为 null 时不调用.name
//null
//Jack

```

### 猫王操作符

Groovy 会将三元操作符的操作数强制转为 boolean
`?:` 是三元操作符的简写方式

Java 方式

```java
String agentStatus = "Active"
String status = agentStatus != null ? agentStatus : "Inactive"
assert status == "Active"
```

Groovy 方式

```groovy
status = agentStatus ? agentStatus : "Inactive"
assert status == "Active"
```

简写

```groovy
status = agentStatus ?: "Inactive"
assert status == "Active"
```

>A:

>使用猫王操作符替代三元操作符
