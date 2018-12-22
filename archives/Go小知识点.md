---
english_title: go-knowledge
title: Go：小知识点
date: 2018-06-13 12:34:56
---

new() 和 make() 的区别

new() 和 &{} 的区别

<!-- more -->

# new() 和 make() 的区别

## new()

`new` 是内建函数，函数原型为

```
func new(Type) *Type
```

源码的注释

> The new build-in function allocates memory（仅仅分配空间）. The first argument is a type, not a value, and the value returned is a pointer to a newly allocated zero value of that type. 

把一个类型传给 `new` ，`new`会创建一个该类型的零值，并将该零值的**指针**返回。

## make()

`make` 也是内建函数，函数原型为

```
func make(t Type, size ...IntegerType) Type
```

源码的注释

> The make built-in function allocates and initializes an object（分配空间 + 初始化） of type slice, map or chan**(only)**. Like new , the first arguement is a type, not a value. Unlike new, make’s return type is the same as the type of its argument, not a pointer to it. The specification of the result depends on the type. 

`make` 只接收 `slice` `map` `chan` 这三种类型，因为 `slice` `map` `chan` 是 Go 中的引用类型 （Go只有值传递，没有引用传递），而引用类型是可以直接拿来修改的，类似于引用传递，所以 `make` 会将它接收到的引用类型，分配空间，并做初始化的修改，最终返回该**引用类型**。

- Slice : 第二个参数 size 指定了它的长度，此时它的容量和长度相同。你可以传入第三个参数 来指定不同的容量值，但是必须不能比长度值小。比如:  make([]int, 0, 10)
- Map: 根据 size 大小来初始化分配内存，不过分配后的 map 长度为 0。 如果 size 被忽略了，那么会在初始化分配内存的时候 分配一个小尺寸的内存。
- Channel: 管道缓冲区依据缓冲区容量被初始化。如果容量为 0 或者被忽略，管道是没有缓冲区的。

参考

https://studygolang.com/articles/3496

http://sanyuesha.com/2017/07/26/go-make-and-new/

# new() 和 &{} 的区别

对于 `struct` 来说，new() 和 &{} 没有区别

```
type Foo struct {
    name string
    age  int
}

//声明初始化
var foo1 Foo
fmt.Printf("foo1 --> %#v\n ", foo1) //main.Foo{age:0, name:""}
foo1.age = 1
fmt.Println(foo1.age)

//struct literal 初始化
foo2 := Foo{}
fmt.Printf("foo2 --> %#v\n ", foo2) //main.Foo{age:0, name:""}
foo2.age = 2
fmt.Println(foo2.age)

//指针初始化
foo3 := &Foo{}
fmt.Printf("foo3 --> %#v\n ", foo3) //&main.Foo{age:0, name:""}
foo3.age = 3
fmt.Println(foo3.age)

//new 初始化
foo4 := new(Foo)
fmt.Printf("foo4 --> %#v\n ", foo4) //&main.Foo{age:0, name:""}
foo4.age = 4
fmt.Println(foo4.age)

//声明指针并用 new 初始化
var foo5 *Foo = new(Foo)
fmt.Printf("foo5 --> %#v\n ", foo5) //&main.Foo{age:0, name:""}
foo5.age = 5
fmt.Println(foo5.age)
```
