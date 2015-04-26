title: "Step-into-Groovy-09-集合"
date: 2015-04-26 17:21:07
categories: groovy
tags: groovy
toc: true
---

摘要

>创建集合，空集合，添加（<<）及访问元素，+/-，展开操作符，size


## 集合

### 创建集合

```java
def list = ["Groovy", "Java", "Scala"]
assert list instanceof Collection
assert list instanceof ArrayList
```

### 空集合

```java
def list = []
```

### 添加元素

```java
list.add("Rust")
```

或者

```java
list << "Katlin"
```

Groovy 中 `<<` 操作符被重载，以支持向集合中添加元素

或者

```groovy
list.putAt(9, "Python")
```

或者

```java
def list = []
list[10] = "Ruby"
```

### 访问元素

```groovy
list[2]
list.get(2)
list[-1]
list[-1..-2]
```

>A:
>
>使用 "<<" 添加元素，使用 "[]" 访问元素

### 根据原列表返回新列表

```java
def list = ["Groovy", "Java", "Scala"]

// 此操作不会修改原有列表
def nlist = list - ["Ruby", "Scala", "Java"] + "Swift"
```

### Spread Operator

展开操作符为 **`*`**，用于对集合中的每一个元素进行操作后返回新列表

```java
def numbers = [1, 2, 3, 4, 3, 4]
def numbers2 = numbers*.plus(10)
println(numbers)            //[1, 2, 3, 4, 3, 4]
println(numbers2)           //[11, 12, 13, 14, 13, 14]
```

### 获取长度

Groovy 中 List, Map, String 等都统一用 size()来获取长度。


### 常用操作

#### 根据列表创建字符串

```java
def numbers = [1, 2, 3, 4, 3, 4]
println numbers.join(",")   //1,2,3,4,3,4
```

####  获得集合中重复值的个数

```java
def numbers = [1, 2, 3, 4, 3, 4]
println numbers.count(3)    //2
```

#### 其它操作

```java
list = [1, 2, 3, [4, 5]]
println list.flatten()                  //展开后返回新列表，->[1, 2, 3, 4, 5]
println list.intersect([3, 4, 5])       //返回新列表包含交集, ->[3]
println list.pop()                      //[4, 5]
println list.reverse()                  //[3, 2, 1]
println list.sort()                     //返回反转的新列表, ->[1, 2, 3]
```
