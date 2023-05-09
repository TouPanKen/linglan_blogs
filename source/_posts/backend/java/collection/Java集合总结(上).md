---
title: Java集合总结(上)
link: backend-java-collection-Java集合总结(上)
catalog: true
mermaid: true
lang: cn
date: 2022-07-31 01:02:56 
tags:
- 后端
- Java集合
categories:
- [后端,Java,集合]
---

# 集合概述

## 为什么要用集合？

当我们需要保存一组类型相同的数据的时候，我们应该是用一个容器来保存，这个容器就是`数组`，但是，使用数组存储对象具有一定的弊端， 因为我们在实际开发中，存储的数据的类型是多种多样的，于是，就出现了`集合`，`集合`同样也是用来存储多个数据的。

`数组`的缺点是一旦声明之后，长度就不可变了；同时，声明数组时的数据类型也决定了该数组存储的数据的类型；而且，数组存储的数据是有序的、可重复的，特点单一。 但是`集合`提高了数据存储的灵活性，Java 集合不仅可以用来存储不同类型不同数量的对象，还可以保存具有映射关系的数据。

## Java 集合概述

Java 中的集合可以理解为"容器“，它主要是由这两大接口派生而来：`集合(Collection)`,主要用于存储一个元素的集合 另一个是 `图(Map)`，主要用于存储键/值对。
对于 `Collection` 接口来说，下面还有三个主要的子接口：`List`，`Set`，`Queue`。

Java集合架构如下图所示：

![Java集合.png](https://s2.loli.net/2023/05/05/he3Yr9Nz25FMpOT.png)

## List

在集合类中，`List` 是最基础的一种集合：List集合是有序的，程序员可对其中的每个元素的插入位置进行精确的控制，可以通过索引来访问元素，遍历元素。

在`List`集合中，我们经常用到的是`ArrayList`和`LinkedList`这两个类。

其中，`ArrayList`底层通过数组实现，随着元素的增加而动态扩容。而`LinkedList`底层通过链表来实现，随着元素的增加不断向链表的后端增加节点。

## Set

Java Set接口是`Java Collections Framework`的成员。

`Set`:注重独一无二的性质,该体系集合可以知道某物是否已近存在于集合中,不会存储重复的元素,允许包括值为`null`的元素，但是最多只能有一个`null`元素。用于存储无序(存入和取出的顺序不一定相同)元素，值不能重复。

Set集合下最常见的集合类有三个：`HashSet`、`TreeSet`、`LinkedHashSet`。

我们看看对比这三者的区别和相同点

### 相同点：

- 不存在重复的元素
- 非线程安全的，多线程编程时要额外对这三者进行同步。
- `Fail-Fast` 迭代器。迭代器创建后发生变化的原因不是因为迭代器的 `remove` 方法，会抛出 `ConcurrentModificationException` 异常，对于删除元素可以使用迭代器的 `remove` 方法。

### 不同点：

- 性能
  - `HashSet` 的处理速度是最快，其次是`LinkedHashSet`(几乎是和HashSet相同)，`TreeSet`由于是插入元素时需要排序，因此`TreeSet`的处理速度相对要慢一些。
- 元素排序
  - `HashSet` 不维持元素的顺序，`LinkedHashSet` 元素顺序遵循插入顺序，`TreeSet` 元素顺序遵循排序顺序。
- 内部实现
  - `HashSe`t 基于 `HashMap`，`LinkedHashSet` 基于 `HashSet` 和 `LinkedList`，`TreeSet` 基于 `NavigableMap`，`Java` 默认为 `TreeMap`。
- 是否允许null值
  - `HashSet` 和 `LinkedHashSet` 都允许 `null` 元素，但 `TreeSet` 不允许 `null` 元素，而且当向 `TreeSet` 插入 `null` 元素时，`TreeSet` 使用 `compareTo` 方法与 `null` 元素进行比较，将会出现 `java.lang.NullPointerException`。
- 比较
  - `HashSet` 和 `LinkedHashSet` 使用 `equals` 方法来进行比较；而 `TreeSet` 使用 `compareTo` 方法进行比较来维持元素顺序。这就是为什么 `compareTo` 方法需要与 `equals` 方法实现保持一致的原因。当 `compareTo` 方法与 `equals` 方法实现不一致时，这违反了实现 `Set` 的特点（不允许元素重复）。

## Queue



## Map



## List，Set，Queue，Map的区别

- `List`
- `Set`
- `Queue`
- `Map`

## 如何选用集合？


## Collection 子接口 List

### ArrayList和Vector的区别



### ArrayList和LinkedList的区别



## Collection 子接口 Set

### Comparable 和 Comparator 的区别



### 无序性和不可重复性的含义是什么.



## Collection 子接口 Queue

### Queue 与 Deque 的区别



### ArrayDeque 与 LinkedList 的区别



### PriorityQueue



# 总结



# 参考
- JavaGuide(java面试+学习指南)：https://javaguide.cn/java/collection/java-collection-questions-01.html#java-%E9%9B%86%E5%90%88%E6%A6%82%E8%A7%88
- TreeSet, LinkedHashSet 和 HashSet 差异对比:https://xie.infoq.cn/article/e1b42f77c465f501ba3727c1d


