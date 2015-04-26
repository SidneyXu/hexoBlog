title: "Step-into-Groovy-11-类"
date: 2015-04-26 17:23:58
categories: groovy
tags: groovy
toc: true
---

摘要

>定义类，默认构造方法，"."，不可变类

## 类

### 定义类

```groovy
class Song {
  def name
  def artist
  def genre

  def show() {
    "${name}:${artist}"
  }
}
```

Grooy 中默认访问权限都是 public

### 默认构造方法

当一个类被定义时，Groovy 会自动根据成员变量生成对应的默认构造方法

```groovy
def song = new Song(artist: "Peter", name: "Hello World")
```

### Setter 和 Getter

Groovy 对象通过 `.` 调用属性实际调用的是对应的 setter 和 getter 方法
Groovy 自动对这些属性做了封装处理

```groovy
class Song {
  def name
  def artist
  def genre

  def setArtist(p) {
    artist = p.toUpperCase()
  }
}

def song = new Song(artist: "Peter", name: "Hello World")
song.artist = "Tim"
println(song.artist)                //TIM
```

### 不可变类

#### 特点

- 不可变类使用 `@Immutable` 进行修饰
- 不可变类成员属性只能在构造对象时设置，之后不能进行更改
- 不可变类的成员属性定义时必须明确指明类型，不能使用 def 定义

#### 使用

```groovy
@Immutable
class ImmutSong {
  String name
  String artist
  String genre

  def show(){
    artist
  }
}

ImmutSong song = new ImmutSong(artist: "Peter")
//        song.name="Hello"		error，不能进行修改
//        song.artist="Jack"	error，不能进行修改
println song.show()     //Peter
```

>A：

>尽量使用不可变类
