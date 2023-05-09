---
title: ArrayList底层
link: backend-java-collection-ArrayList底层
catalog: true
mermaid: true
lang: cn
date: 2022-07-31 01:02:56
tags:
  - 后端
  - Java集合
  - 源码分析
categories:
  - [ 后端,Java,集合,源码分析 ]
---

# ArrayList简介

`ArrayList`的底层是`数组队列`，相当于是`动态数组`。与`Java`的中的数组相比，`ArrayList`
它的容量能够动态的增长。在添加大量元素前可以使用`ensureCapacity`来操作添加`AyyayList`实例容量。
`ArrayList`继承于`AbstractList`,实现了`List`,`RandomeAccess`,`Cloneable`,`Serializable` 这些接口。实现了`Serializable`
接口支持实例化，能够通过实例化传输，实现了`RandomAccess`
接口支持快速随机访问，实际上就是通过下标序号进行快速进行访问,实现`Cloneable`接口，可以被克隆。`ArrayList`实现了`List`
提供了相关的`添加`，`删除`,`修改`,`遍历`等功能。
`ArrayList`和`Vector`不同的是`ArrayList`
中的线程操作不安全的！只能用在单线程的环境下，多线程环境下可以考虑使用`Collections.synchronizedList(List)`
函数返回一个安全的`ArrayList`类，也可以使用`concurrent`并发包下的`CopyOnWriteArrayList`类。

# ArrayList核心源码

## 底层存储数据结构

```java

/**
 * The array buffer into which the elements of the ArrayList are stored.
 * The capacity of the ArrayList is the length of this array buffer. Any
 * empty ArrayList with elementData == DEFAULTCAPACITY_EMPTY_ELEMENTDATA
 * will be expanded to DEFAULT_CAPACITY when the first element is added.
 */
transient Object[] elementData; // non-private to simplify nested class access

/**
 * The size of the ArrayList (the number of elements it contains).
 *
 * @serial
 */
private int size;

```

- Object 数据类型
- 当前数据对象存放地方，当前对象不参与序列化
- 这个关键字最主要的作用就是当序列化时，被transient修饰的内容将不会被序列化

## 构造函数

```java
/**
 * Constructs an empty list with the specified initial capacity.
 *
 * @param  initialCapacity  the initial capacity of the list
 * @throws IllegalArgumentException if the specified initial capacity
 *         is negative
 */
public ArrayList(int initialCapacity) {
    if (initialCapacity > 0) {
        this.elementData = new Object[initialCapacity];
    } else if (initialCapacity == 0) {
        this.elementData = EMPTY_ELEMENTDATA;
    } else {
        throw new IllegalArgumentException("Illegal Capacity: "+
                                           initialCapacity);
    }
}

/**
 * Constructs an empty list with an initial capacity of ten.
 */
public ArrayList() {
    this.elementData = DEFAULTCAPACITY_EMPTY_ELEMENTDATA;
}

/**
 * Constructs a list containing the elements of the specified
 * collection, in the order they are returned by the collection's
 * iterator.
 *
 * @param c the collection whose elements are to be placed into this list
 * @throws NullPointerException if the specified collection is null
 */
public ArrayList(Collection<? extends E> c) {
    elementData = c.toArray();
    if ((size = elementData.length) != 0) {
        // c.toArray might (incorrectly) not return Object[] (see 6260652)
        if (elementData.getClass() != Object[].class)
            elementData = Arrays.copyOf(elementData, size, Object[].class);
    } else {
        // replace with empty array.
        this.elementData = EMPTY_ELEMENTDATA;
    }
}
```

## 自动扩容

每当向数组中添加元素时，都要去检查添加后元素的个数是否会超出当前数组的长度，如果超出，数组将会进行扩容，以满足添加数据的需求。数组扩容通过一个公开的方法`ensureCapacity(int minCapacity)`
来实现。在实际添加大量元素前，我也可以使用`ensureCapacity`来手动增加`ArrayList`
实例的容量，以减少递增式再分配的数量。数组进行扩容时，会将老数组中的元素重新拷贝一份到新的数组中，每次数组容量的增长大约是其原容量的`1.5`
倍。这种操作的代价是很高的，因此在实际使用时，我们应该尽量避免数组容量的扩张。当我们可预知要保存的元素的多少时，要在构造`ArrayList`
实例时，就指定其容量，以避免数组扩容的发生。或者根据实际需求，通过调用`ensureCapacity`方法来手动增加`ArrayList`实例的容量。

```java
/**
 * Increases the capacity of this <tt>ArrayList</tt> instance, if
 * necessary, to ensure that it can hold at least the number of elements
 * specified by the minimum capacity argument.
 *
 * @param   minCapacity   the desired minimum capacity
 */
public void ensureCapacity(int minCapacity) {
    int minExpand = (elementData != DEFAULTCAPACITY_EMPTY_ELEMENTDATA)
        // any size if not default element table
        ? 0
        // larger than default for default empty table. It's already
        // supposed to be at default size.
        : DEFAULT_CAPACITY;

    if (minCapacity > minExpand) {
        ensureExplicitCapacity(minCapacity);
    }
}

private void ensureCapacityInternal(int minCapacity) {
    if (elementData == DEFAULTCAPACITY_EMPTY_ELEMENTDATA) {
        minCapacity = Math.max(DEFAULT_CAPACITY, minCapacity);
    }

    ensureExplicitCapacity(minCapacity);
}

private void ensureExplicitCapacity(int minCapacity) {
    modCount++;

    // overflow-conscious code
    if (minCapacity - elementData.length > 0)
        grow(minCapacity);
}

/**
 * The maximum size of array to allocate.
 * Some VMs reserve some header words in an array.
 * Attempts to allocate larger arrays may result in
 * OutOfMemoryError: Requested array size exceeds VM limit
 */
private static final int MAX_ARRAY_SIZE = Integer.MAX_VALUE - 8;

/**
 * Increases the capacity to ensure that it can hold at least the
 * number of elements specified by the minimum capacity argument.
 *
 * @param minCapacity the desired minimum capacity
 */
private void grow(int minCapacity) {
    // overflow-conscious code
    int oldCapacity = elementData.length;
    int newCapacity = oldCapacity + (oldCapacity >> 1);
    if (newCapacity - minCapacity < 0)
        newCapacity = minCapacity;
    if (newCapacity - MAX_ARRAY_SIZE > 0)
        newCapacity = hugeCapacity(minCapacity);
    // minCapacity is usually close to size, so this is a win:
    elementData = Arrays.copyOf(elementData, newCapacity);
}

private static int hugeCapacity(int minCapacity) {
    if (minCapacity < 0) // overflow
        throw new OutOfMemoryError();
    return (minCapacity > MAX_ARRAY_SIZE) ?
        Integer.MAX_VALUE :
        MAX_ARRAY_SIZE;
}
```

# ArrayList源码分析

## add(),addAll()

`ArrayList`的两个添加的方法是`add(E e)`和`add(int index,E e)`
。这两个方法都是向容器中添加新的元素，这可能会导致容量不足，因此在添加元素之前，都需要进行剩余空间检查，如果需要则自动扩容。扩容操作最终是通过grow()
方法完成的。

```java
/**
 * Appends the specified element to the end of this list.
 *
 * @param e element to be appended to this list
 * @return <tt>true</tt> (as specified by {@link Collection#add})
 */
public boolean add(E e) {
    ensureCapacityInternal(size + 1);  // Increments modCount!!
    elementData[size++] = e;
    return true;
}
private void ensureCapacityInternal(int minCapacity) {
        ensureExplicitCapacity(calculateCapacity(elementData, minCapacity));
}
private static int calculateCapacity(Object[] elementData, int minCapacity) {
    // 这里就是DEFAULTCAPACITY_EMPTY_ELEMENTDATA 和
    // EMPTY_ELEMENTDATA 最主要的区别。
    if (elementData == DEFAULTCAPACITY_EMPTY_ELEMENTDATA) {
        // 默认构造第一次add返回10。
        return Math.max(DEFAULT_CAPACITY, minCapacity);
    }
    // 带参为0构造第一次add返回 1 （0 + 1）。
    return minCapacity;
}
 private void ensureExplicitCapacity(int minCapacity) {
    modCount++;

    // overflow-conscious code
    if (minCapacity - elementData.length > 0)
        grow(minCapacity);
}

 /**
 * Increases the capacity to ensure that it can hold at least the
 * number of elements specified by the minimum capacity argument.
 *
 * @param minCapacity the desired minimum capacity
 */
private void grow(int minCapacity) {
    // overflow-conscious code
    int oldCapacity = elementData.length;
    int newCapacity = oldCapacity + (oldCapacity >> 1);
    if (newCapacity - minCapacity < 0)
        newCapacity = minCapacity;
    if (newCapacity - MAX_ARRAY_SIZE > 0)
        newCapacity = hugeCapacity(minCapacity);
    // minCapacity is usually close to size, so this is a win:
    elementData = Arrays.copyOf(elementData, newCapacity);
}

// 这是一个本地方法，由C语言实现。
public static native void arraycopy(Object src,  // 源数组
    int  srcPos, // 源数组要复制的起始位置
    Object dest, // 目标数组（将原数组复制到目标数组）
    int destPos, // 目标数组起始位置（从目标数组的哪个下标开始复制操作）
    int length   // 复制源数组的长度
    );

/**
 * Inserts the specified element at the specified position in this
 * list. Shifts the element currently at that position (if any) and
 * any subsequent elements to the right (adds one to their indices).
 *
 * @param index index at which the specified element is to be inserted
 * @param element element to be inserted
 * @throws IndexOutOfBoundsException {@inheritDoc}
 */
public void add(int index, E element) {
    rangeCheckForAdd(index);

    ensureCapacityInternal(size + 1);  // Increments modCount!!
    System.arraycopy(elementData, index, elementData, index + 1,
                     size - index);
    elementData[index] = element;
    size++;
}
```

## remover()

`remover()`的方法也有两个版本，一个是`remover(int index)`删除指定的位置的元素，另一个是`remover(object o)`删除第一个满足`o.equals(elementData[index])` 的元素。删除的操作是`add()`操作的逆过程，需要将删除点之后的元素向前移动一个位置。需要注意的是为了让`GC`起作用，必须显式的为最后一个位置赋`null`值。

```java
public E remove(int index) {
    rangeCheck(index);
    modCount++;
    E oldValue = elementData(index);
    int numMoved = size - index - 1;
    if (numMoved > 0)
        System.arraycopy(elementData, index+1, elementData, index, numMoved);
    elementData[--size] = null; //清除该位置的引用，让GC起作用
    return oldValue;
}
```

## Fail-Fast机制:

`Fail-Fast机制`,即使就是 快速失败机制，是Java集合(Collection)中的一种错误检测机制。当在迭代集合的过程中该集合在结构上发生改变的时候，就会有可能就会发生`Fail-Fast`，即抛出`ConcurrentModificationException`异常。`Fail-Fast机制`并不能保证在不同步的修改下一定会抛出异常，这个机制最多就是一般用于检测`Bug`。

# 总结

- ArrayList底层数据结构是数组，无容量的限制（会扩容）。当创建ArrayList对象时，底层初始化了一个空数组，数组是Object类型，数组名是elementData。当第一次添加元素时，数组长度扩容为10。
- 当第11次添加时，会触发扩容机制，其实就是调用 grow方法，扩容为原数组长度的1.5倍。
- 每次扩容时，都是创建一个新数组，将老数组的元素通过 Arrays工具类复制到新数组中。elementData 指向了新数组。
- 扩容不是在老数组基础上拼接，而创建一个1.5倍长度的新数组，并把老数组的元素复制到新数组中。
- ArrayList 线程不安全。

# 参考：
- Collection - ArrayList 源码解析：https://pdai.tech/md/java/collection/java-collection-ArrayList.html#%E5%BA%95%E5%B1%82%E6%95%B0%E6%8D%AE%E7%BB%93%E6%9E%84
- Java ArrayList底层实现原理源码详细分析Jdk8：https://www.cnblogs.com/neverth/p/11786048.html
- ArrayList自动扩容原理：https://blog.csdn.net/weixin_44031029/article/details/122265768