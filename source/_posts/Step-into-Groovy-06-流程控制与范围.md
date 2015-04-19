title: "Step-into-Groovy-06-流程控制与范围"
date: 2015-04-19 09:43:02
categories: groovy
tags: groovy
toc: true
---

摘要

>布尔环境，Switch（类型匹配，范围匹配），For，Range

## 流程控制与范围

### 流程控制

#### If

Groovy 中在 If 等类似的布尔环境中，表达式会被自动转为布尔值。规则为 `0`, `null` 及 `empty` 为 **false**，其余为 **true**。

```groovy
def i = 0
if (i) {
  println true
} else {
  println false
}

def list = []
if (list) println true else println false
```

>A:
>
>布尔环境中使用自动转换

#### Switch

```groovy
switch (var) {
  case 0: println 0
      break
  case 11..20: println "11..20"	//左右都包含
      break
  case [1, 2, 3]: println '[1,2,3]'
      break
  case Float: println 'Float'
      break
  case { it % 3 == 0 }: println 'Closure'
      break
  case ~'[0-9]{3}': println 'Regex'
      break
  default: println 'Default'
}

test(0)     //0
test(20)    //11..20
test(11)    //11..20
test(30)    //Closure
test(2)     //[1,2,3]
test(1.2f)  //Float
test(100)   //Regex
test(1000)  //Default
```

#### For

传统的 for 循环

```groovy
for (i = 0; i < 5; i++) {
    println val
}
```

基于 Range 的 for 循环

```groovy
for (i in 0..< 5) {
    println val
}
```

in 的目标可以是范围，映射或者 GString

### Range 范围

Range 是特殊的 List

```java
def range = 0..4
println range.class         //class groovy.lang.IntRange
assert range instanceof List
```

Range 有以下形式

左右都包含

```groovy
0..3			//表示0,1,2,3
```

左闭右开

```groovy
0..<3			//表示0,1,2
```

除了数字，也可以使用字母

```groovy
"a".."e"		//表示 a,b,c,d,e
```

>A:
>
>简单类型时，使用 Range 代替 List