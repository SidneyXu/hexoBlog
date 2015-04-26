title: "Step-into-Groovy-10-映射"
date: 2015-04-26 17:22:38
categories: groovy
tags: groovy
toc: true
---

摘要

>创建映射，空映射，访问元素

## 映射

### 创建映射

```java
def map = [name: "Peter", "age": 12, "national": "USA"]
println map.getClass()      //class java.util.LinkedHashMap
```

实际创建的是 LinkedHashMap对象，key 可以直接是名字或字符串

###  空映射

```java
def emptyMap = [:]
```

### 添加元素

```groovy
//map.put(uid, 1000)    error
map.put("id", 10)
```

注意此时与创建时不同，不能直接使用名字

或者

```groovy
map.sex = "boy"
```

或者

```groovy
//map[height] = 100   error
map["height"] = 180
```

此时也不能使用名字

