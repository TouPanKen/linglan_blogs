---
title: Java基础总结(中)
link: backend-java-foundation-Java基础总结(中)
catalog: true
lang: cn
date: 2022-07-31 01:02:56 
tags:
- 后端
- Java基础
categories:
- [后端,Java,基础]
---

# 面向对象

## 面向对象和面向过程的区别

面向对象编程（Object Oriented Programming，简称 OOP）和面向过程编程（Procedure Oriented Programming，简称 POP）是两种不同的编程思想。

在面向过程编程中，程序被视为一连串的函数调用、数据流和变量赋值等基本的函数式执行步骤。程序员需要根据问题的需求，设计出相应的函数和数据结构，通过对这些函数和数据的组合和调用，来实现整个程序的功能。

相比之下，在面向对象编程中，程序员则更加关注于对象的角度，将程序看作是一系列对象之间的交互和消息传递。程序员需要先定义出各种对象以及它们各自的属性和方法，然后通过对象之间的方法调用和消息传递来完成程序的执行。

具体而言，面向对象编程由以下特点：

1. 抽象：面向对象编程通过将真实世界映射到程序实体中实现抽象化，将复杂的问题简化为对象和类的关系。

2. 封装：面向对象编程中，对象封装了数据和方法，隐藏了实现细节，只暴露出公共的接口，提高了代码的可维护性和可扩展性。

3. 继承：面向对象编程中，一个类可以从另一个类继承属性和方法，从而实现代码重用和扩展。

4. 多态：面向对象编程中，不同的对象可以具有相同的方法名，但是表现出不同的行为。这样实现了代码复用和灵活性。

而面向过程编程则更加侧重于以下特点：

1. 强调步骤和流程：面向过程编程通过分解问题，将大问题分解为小问题，逐步完成整个程序的构建。

2. 数据为中心：面向过程编程中，程序员会自然而然地设计一些基本的数据结构和算法，然后通过函数调用来操作这些数据结构达到预期目的。

3. 通常需要自行管理资源：在面向过程编程中，通常需要手动管理资源，如内存分配、释放等。

总而言之，面向对象编程和面向过程编程都有其优缺点和适应场景，在实际编程中需要根据问题的需求和自己的经验和喜好选择合适的编程范式。

## 创建一个对象用什么运算符?

在 Java 中，我们使用关键字 `new` 来创建一个对象。具体来说，创建一个对象需要执行以下操作：

1. 使用 `new` 关键字创建一个对象。
2. 使用类名后面紧跟的小括号调用构造函数初始化这个对象。

例如，在下面的代码中，我们使用 `new` 关键字创建了一个 `Person` 类的对象 `person` ：

``` Java
Person person = new Person();
```

其中 `Person()` 表示 `Person` 类的默认构造函数，它会在对象创建之后自动被调用。如果需要传递参数给构造函数进行初始化，则可以在小括号中传入相应的参数，如下所示：

``` Java
Person person = new Person("张三", 18);
```

这里我们调用带有两个参数的 `Person` 类构造函数，将 `"张三"` 和 `18` 作为参数传入，以便在对象创建时进行初始化。

需要注意的是，只要调用了构造函数，就会返回一个新的对象，该对象在内存中分配了空间，并按照构造函数的定义进行了初始化。可以使用引用变量来访问这个对象，进而进行相关的操作。

## 对象实体与对象引用有何不同?

在 Java 中，对象实体和对象引用是两个不同的概念。

对象实体（Object）指的是在内存中具体存在的、占据一定空间的一个实例。当使用 `new` 关键字创建一个对象时，就会在内存中分配一块空间来存储这个对象，并返回一个对该对象的引用。例如：

``` Java
Person person = new Person("张三", 18);
```

其中，`new Person("张三", 18)` 创建了一个 `Person` 类的对象实体，并返回对该对象的引用 `person`。此时，`person` 指向这个对象实体。

而对象引用（Reference）则是指一个变量所持有的一个对象的句柄，它指向了内存中的一个对象实体。引用不是对象本身，而是一个指向对象的指针。例如：

``` Java
Person person1 = new Person("张三", 18);
Person person2 = person1;
```

在上面的代码中，我们创建了两个引用变量 `person1` 和 `person2`，并将它们都指向了同一个 `Person` 类的对象实体。此时，`person1` 和 `person2` 都指向了相同的对象实体。

需要注意的是，Java 中所有对象的访问都是通过对象引用来实现的。每个引用变量只能指向一个对象实体，但是不同的引用变量可以指向同一个对象实体，即多个对象引用可以共同指向同一个对象实体。这种特性使得对象之间的共享和交互变得更加容易和灵活。

## 对象的相等和引用相等的区别

在 Java 中，对象的相等和引用相等是两个不同的概念：

1. 引用相等（Reference Equality）：当两个对象引用指向内存中的同一对象实例时，我们称它们是引用相等的。可以使用 `==` 运算符来检测两个对象的引用是否相等。

例如：

``` Java
Person person1 = new Person("张三", 18);
Person person2 = person1;

if (person1 == person2) {
    System.out.println("person1 和 person2 是引用相等的");
}
```

上面的代码中，由于 `person2` 引用与 `person1` 指向同一个对象实例，因此它们是引用相等的。

2. 对象相等（Object Equality）：当两个对象在逻辑上认为是相等的，即它们包含的数据或状态相同，我们称它们是对象相等的。可以使用 `equals()` 方法来检测两个对象是否相等。

例如：

``` Java
Person person1 = new Person("张三", 18);
Person person2 = new Person("张三", 18);

if (person1.equals(person2)) {
    System.out.println("person1 和 person2 是对象相等的");
}
```

上面的代码中，虽然 `person1` 和 `person2` 的引用不相等，但是它们包含的数据相同，因此它们是对象相等的。需要注意的是，在使用 `equals()` 方法比较两个对象相等性时，需要确保该方法已经被正确地实现，即根据对象的内容或状态进行比较。

需要注意的是，在 Java 中，如果两个对象是引用相等的，则它们一定是对象相等的。但是如果两个对象是对象相等的，则它们不一定是引用相等的。这是因为在 Java 中，对象相等只依赖于对象的内容或状态，而与对象在内存中的位置无关。

## 如果一个类没有声明构造方法，该程序能正确执行吗?

如果一个类没有显式地声明任何构造方法，则 Java 编译器会自动生成一个默认的无参构造方法。这个默认构造方法的访问修饰符与类的访问修饰符相同，如果类是公共类，则默认构造方法也是公共的。

因此，即使一个类没有显式地定义构造方法，Java 编译器会自动生成一个默认构造方法，程序仍然可以正确执行。例如：

``` Java
public class MyClass {
    private int value;

    public int getValue() {
        return value;
    }
}

// 创建 MyClass 对象
MyClass myObject = new MyClass();

// 调用 getValue() 方法
int result = myObject.getValue();
```

在上面的代码中，MyClass 类没有显式地定义构造方法，但是在创建 MyClass 对象时，Java 编译器会自动生成一个默认的无参构造方法。然后我们可以使用 `myObject` 引用来调用 `getValue()` 方法，程序可以正确地执行。

需要注意的是，如果一个类有显式声明了构造方法，那么在创建对象时就必须使用其中一个构造方法进行初始化，否则编译器会报错。因此，在设计一个类时，应该根据具体需要显式地定义构造方法，以确保类的正确性和可靠性。

## 构造方法有哪些特点？是否可被 override?

构造方法是一种特殊的方法，用于创建对象并初始化对象的成员变量。它具有以下特点：

1. 方法名与类名相同：构造方法的方法名必须和它所在的类名相同。

2. 没有返回类型：构造方法没有返回类型，包括 `void` 也不允许。

3. 可以被重载：同一个类中可以定义多个构造方法，它们之间可以根据不同的参数列表进行重载。

4. 执行顺序：在使用 `new` 关键字创建对象时，Java 会自动调用相应的构造方法来初始化对象的成员变量，构造方法的执行顺序是从父类到子类，即先执行父类的构造方法，然后再执行子类的构造方法。

5. 可以访问非静态变量和方法：构造方法可以访问类的非静态成员变量和方法，包括私有成员（如果在同一个类中）。

6. 可以设置访问修饰符：构造方法可以使用访问修饰符来控制其访问范围，例如 `public`、`protected`、`private` 或默认访问修饰符。

需要注意的是，构造方法不能被显式地调用，它只能在使用 `new` 关键字创建对象时被隐式地调用，用于初始化对象的成员变量。

此外，构造方法可以被重写（Override），但是它们的重写规则与普通方法不同。子类的构造方法不能直接重写父类的构造方法，但是可以通过调用父类的构造方法来实现对父类的初始化，这种方式称为“调用父类构造方法”或“super()”语句。例如：

``` Java
public class SuperClass {
    public SuperClass(int value) {
        // 父类构造方法
    }
}

public class SubClass extends SuperClass {
    public SubClass(int value) {
        super(value); // 调用父类构造方法
        // 子类构造方法
    }
}
```

在上面的代码中，子类 `SubClass` 调用了其父类 `SuperClass` 的构造方法来初始化父类的成员变量，然后再执行自身的构造方法来初始化子类的成员变量。

# 面向对象三大特征

面向对象编程的三大特征是：封装、继承和多态。

1. 封装：封装是把对象的属性和行为结合起来，形成一个不可分割的个体，并对外部访问进行限制。封装可以隐藏对象的内部细节，只对外暴露必要的接口，提高了代码的安全性和可维护性。例如，Java 中的类就是一种封装机制。

2. 继承：继承是利用已有类的定义，在此基础上创建新的类。通常情况下，子类继承父类的属性和方法，但也可以在此基础上进行修改或扩展。继承可以避免重复编写代码，提高了代码的重用性和可扩展性。例如，Java 中的类可以使用关键字 "extends" 来实现继承，从而扩展其功能。

3. 多态：多态是指同一种类型的对象，在不同的情况下表现出不同的形态和行为。多态性包括编译时多态性和运行时多态性，前者是指方法的重载（Overload），后者是指方法的覆盖（Override）。多态可以提高代码的灵活性和可扩展性，使得程序更容易被修改和扩展，但也增加了代码的复杂度和理解难度。

总之，封装、继承和多态是面向对象编程的三大特征，它们分别体现了抽象化、继承、多样化等思想，是面向对象编程的核心概念。掌握这三个特征可以帮助我们编写出更加健壮、灵活、易于维护的面向对象程序。

## 接口和抽象类有什么共同点和区别？

接口（Interface）和抽象类（Abstract Class）是面向对象编程中常用的两种机制，它们有一些共同点，也有一些区别。

1. 共同点：

- 都不允许被实例化：接口和抽象类都不能直接被实例化，只能用于派生其他类。

- 都可以定义抽象方法：接口和抽象类都可以定义抽象方法，子类必须实现这些抽象方法才能正常运行。

2. 区别：

- 实现方式不同：接口是一种特殊的类，它只定义了一组抽象方法和常量，并没有实现任何方法，而抽象类是一个普通的类，可以有成员变量、非抽象的成员方法和构造函数等。

- 继承方式不同：接口是通过 `implements` 关键字来实现继承，一个类可以同时实现多个接口；而抽象类是通过 `extends` 关键字来实现继承，一个类只能继承一个抽象类。

- 权限控制不同：接口中定义的方法默认都是 public 的，接口和其中的方法都不能被 final、static、private 或 protected 修饰；而抽象类中定义的方法可以有不同的访问权限，并且可以被 final、static 或 protected 修饰。

- 设计目的不同：接口的设计目的是为了实现类之间的松耦合和多态性，接口通常定义了一组功能接口，由具体的类来实现这些接口；而抽象类的设计目的是为了定义一些基本的行为和属性，让子类来继承和扩展使用。

因此，在选择接口或抽象类时，需要根据具体的需求和设计目的来做出选择。如果需要定义一个纯粹的接口，用来规范子类的行为，可以选择使用接口；如果需要提供一些公共的属性和行为，并可以通过继承来进行扩展和实现，则可以选择使用抽象类。

## 深拷贝和浅拷贝区别了解吗？

深拷贝（Deep Copy）和浅拷贝（Shallow Copy）是常见的数据拷贝方式，它们之间的区别如下：

1. 浅拷贝：

浅拷贝是指在拷贝对象时，只复制对象本身和其中包含的指针等基本类型数据，而不复制指针所指向的数据。也就是说，当源对象中有引用类型的成员变量时，浅拷贝仅仅复制了该成员变量的引用，并没有创建新的对象。

例如，假设有一个对象 A，其中包含一个成员变量 B，而 B 是一个指向另一个对象的指针。如果我们对 A 进行浅拷贝，那么 A' 中的 B 成员变量仍然会指向原来的对象，也就是说 A 和 A' 会共享同一个 B 对象。

2. 深拷贝：

深拷贝是指在拷贝对象时，不仅复制对象本身和其中包含的基本类型数据，还会递归地复制所有引用类型数据，直到所有的数据都被复制为止。也就是说，当源对象中有引用类型的成员变量时，深拷贝会递归地创建新的对象，而不是简单地复制引用。

例如，假设有一个对象 A，其中包含一个成员变量 B，而 B 是一个指向另一个对象的指针。如果我们对 A 进行深拷贝，那么 A' 中的 B 成员变量会创建一个新的对象，并且该对象与原来的对象完全相同，也就是说 A 和 A' 不会共享同一个 B 对象。

3. 区别：

- 浅拷贝只复制对象本身和其中包含的基本类型数据，而不复制引用类型数据；深拷贝则会递归地复制所有引用类型数据。

- 浅拷贝的源对象和目标对象共享同一份引用类型数据，对其中一个对象的修改会影响另一个对象；深拷贝则不会共享任何数据，每个对象都有自己独立的数据副本。

- 浅拷贝的操作通常比深拷贝快速并且占用的存储空间较少，因为它不需要递归地创建新的数据对象；深拷贝则需要复制完整的数据结构，因此可能会更慢并且占用更多的存储空间。

总之，深拷贝和浅拷贝都是常见的数据拷贝方式，在实际编程中需要根据具体情况来选择使用哪种方式，以达到最优的效果。

## 什么是引用拷贝？

引用拷贝（Reference Copy）指的是在将一个引用类型的变量赋值给另一个变量时，仅仅复制了该变量引用的地址，而没有创建新的数据对象。也就是说，新变量和旧变量都是指向同一个对象的引用，它们共享同一份数据。

例如，假设有一个数组 a，其中包含若干个元素。现在我们定义了一个变量 b，并将其指向数组 a，这时候 b 就是 a 的一个引用，两者指向同一个数据对象。如果我们对数组 a 进行修改，那么通过变量 b 也可以访问到修改后的数据。

引用拷贝通常用于传递大型的数据对象，避免进行不必要的数据复制操作。另外，在面向对象编程中，类的成员变量通常都是引用类型的，因此在定义和使用类的对象时，需要注意引用拷贝的影响。

需要注意的是，引用拷贝仅仅复制了变量本身的引用地址，并没有复制数据对象本身。因此，如果我们通过一个引用变量修改了数据对象，那么其他引用变量也会受到影响。这一点需要在实际编程中特别注意，以避免潜在的错误和不一致性问题。

# Object

## Object 类的常见方法有哪些？

Object 类是所有 Java 类的超类，它定义了所有对象都具有的基本行为和属性。这些基本行为和属性包括以下常见方法：

1. getClass()：返回当前对象所属的类的 Class 对象。

2. hashCode()：返回对象的哈希码（Hash Code），用于对对象进行散列操作。

3. equals(Object obj)：比较两个对象是否相等（内容、地址等）。

4. toString()：返回对象的字符串表示。

5. clone()：创建并返回一个对象的副本，需要实现 Cloneable 接口。

6. finalize()：在对象被垃圾回收之前调用，用于完成对象的清理工作。

7. notify() 和 notifyAll()：唤醒等待在该对象上的线程，让其从等待状态转变为就绪状态。

8. wait()：使当前线程等待，在该对象上等待其他线程的通知，直到被唤醒或超时。

需要注意的是，这些方法都是 Object 类中定义的通用方法，也就是说，所有 Java 类都可以使用这些方法。在实际编程中，我们通常会根据需要重写其中的某些方法，以满足特定的业务需求。同时，还需要特别注意一些方法的使用规范和注意事项，以避免潜在的问题和错误。

## == 和 equals() 的区别

在 Java 中，"==" 运算符和 equals() 方法都用于比较两个对象是否相等，但它们之间有着本质的区别。

1. "==" 运算符：

**"=="** 运算符是一个比较运算符，用于比较两个对象的引用地址是否相同。也就是说，当两个对象的引用地址相同时，**"=="** 返回 true，否则返回 false。

例如，假设有两个对象 a 和 b，它们分别指向地址为 0x1234 和 0x5678 的内存空间。此时使用 "==" 运算符比较这两个对象，结果会得到一个布尔值，表示它们是否引用同一个内存地址。

2. equals() 方法：

equals() 方法是一个普通方法，用于比较两个对象的内容是否相等。默认情况下，equals() 方法与 "==" 运算符的效果相同，即比较两个对象的引用地址是否相同。但是，我们可以通过重写 equals() 方法来改变它的比较逻辑，以实现自定义的对象比较方式。

例如，假设有两个对象 a 和 b，它们虽然指向不同的内存地址，但是它们的属性值相同。此时使用 equals() 方法比较这两个对象，如果它们的属性值相同，则返回 true，否则返回 false。

因此，"==" 运算符比较的是对象的引用地址是否相同，而 equals() 方法比较的是对象的内容是否相同。在实际编程中，我们需要根据具体的业务需求来选择使用哪种方式进行对象的比较操作。同时，如果需要自定义对象的比较方式，就需要重写 equals() 方法，并保证其满足 equals() 方法的使用规范和约定。

## hashCode() 有什么用？

在 Java 中，hashCode() 方法用于返回对象的哈希码（Hash Code），它是一个 int 类型的整数。哈希码通常用于对大量数据进行散列操作，以便能够快速地查找和访问数据。

hashCode() 方法有如下几个作用：

1. 作为散列函数：当我们需要将一组数据分成多个桶时，可以使用散列函数把相似的元素放到同一个桶中。hashCode() 方法就是一种常用的散列函数，它根据对象的内容生成一个与其内容相关的哈希码，用于粗略地对对象进行分类和分组。

2. 作为快速查找的依据：在 HashMap、HashSet 等数据结构中，hashCode() 方法通常被用作查找的依据，以快速定位目标对象所在的位置。因为 hashCode() 方法返回的哈希码具有较高的随机性和均匀性，可以尽可能地减少散列表冲突的概率。

3. 作为对象签名的标识：hashCode() 方法也可以作为对象签名（Signature）的标识，用于表示对象的唯一标识符（UID）。在分布式系统、序列化、反射等方面，对象的唯一标识符起着重要的作用，可以确保对象的一致性和正确性。

需要注意的是，hashCode() 方法并不要求返回唯一的哈希码，也就是说，不同对象的哈希码可能会重复。但是，为了提高哈希表等数据结构的性能，哈希码应该具有良好的随机性和均匀性，以避免冲突和性能下降。因此，实现 hashCode() 方法时需要特别注意以下几点：

1. 相同的对象必须返回相同的哈希码。

2. 不同的对象通常应该返回不同的哈希码，以提高散列均匀性。

3. hashCode() 方法的实现应该快速且高效，不要耗费过多的时间和空间。

## 为什么要有 hashCode？

在 Java 中，每个对象都有一个哈希码（Hash Code），它是一个 int 类型的整数。hashCode 的作用主要是为了提高散列算法的效率和减少散列表的冲突。

具体来说，hashCode() 方法可以在散列表等数据结构中快速地查找和访问数据。散列表是一种常用的数据结构，它可以将大量的键值对映射到不同的桶（Bucket）中，以实现快速的插入、查找和删除操作。

在散列表中，每个键值对通常被映射到一个固定的桶中，这个桶的位置可以根据键的哈希码计算得到。因此，如果哈希码具有良好的随机性和均匀性，散列表的性能和效率就会得到很大程度的优化。而哈希码的计算方法通常是通过对对象的内容进行处理和加工，以生成一个与内容相关的整数。

另外，hashCode() 方法还可以作为对象签名（Signature）的标识，用于表示对象的唯一标识符（UID）。在分布式系统、序列化、反射等方面，对象的唯一标识符起着重要的作用，可以确保对象的一致性和正确性。

需要注意的是，在实现 hashCode() 方法时需要遵循以下几个原则：相同的对象必须返回相同的哈希码，不同的对象通常应该返回不同的哈希码，hashCode() 方法的实现应该尽可能快速和高效。

**那为什么 JDK 还要同时提供这两个方法呢？**

在 Java 中，equals() 和 hashCode() 方法是两个不同的方法，它们的作用和使用场景也不同。equals() 方法用于比较两个对象是否相等，而 hashCode() 方法则用于返回对象的哈希码（Hash Code）。

虽然这两个方法的实现看似毫不相关，但实际上它们之间存在一定的联系和依赖。具体来说，为了保证对象的正确性和一致性，我们通常需要同时实现 equals() 和 hashCode() 两个方法，并遵循如下原则：

1. 如果两个对象相等（equals() 方法返回 true），则它们的哈希码必须相等（hashCode() 方法返回的整数值也必须相等）。

2. 如果两个对象不相等（equals() 方法返回 false），则它们的哈希码可以相等，也可以不相等。但是为了提高散列表等数据结构的效率和减少冲突，不同对象的哈希码应该尽量不同，以提高哈希表的查找效率。

由于 equals() 和 hashCode() 两个方法经常被一同使用，因此 JDK 提供了 Object 类中的 hashCode() 方法和 equals() 方法的默认实现。这些默认实现通常基于对象的内存地址计算哈希码和比较对象的相等性，在绝大多数情况下都具有良好的效果和性能。

但是在实际应用中，有些对象可能需要自定义 equals() 和 hashCode() 方法的实现，以满足特定的业务需求和应用场景。比如，对于一个自定义的 Person 类，我们可能希望根据 personId 字段来判断两个 Person 对象是否相等，并基于 personId 计算哈希码。这样可以确保相同 personId 的对象具有相同的哈希码和相等的行为。

**那为什么不只提供 hashCode() 方法呢？**

虽然 hashCode() 方法可以帮助我们快速地比较对象的相等性和提高散列表等数据结构的效率，但是它并不能完全替代 equals() 方法的作用。

实际上，equals() 方法在比较两个对象是否相等时通常比 hashCode() 方法更加精确和准确。因为 equals() 方法可以比较对象的所有属性和字段，并考虑到逻辑上的相等性，而 hashCode() 方法只能计算出一个整数值，无法对对象进行全面的比较和判断。

此外，hashCode() 方法还有一个问题就是哈希冲突（Hash Collision）。由于哈希码是一个有限的整数集合，不同的对象可能会产生相同的哈希码，这种情况称为哈希冲突。哈希冲突会导致散列表等数据结构的查找效率下降，并增加了对象比较的复杂度和难度。

因此，在使用 hashCode() 方法时，我们需要额外地考虑哈希冲突和处理方法，并且根据业务需求和对象特性来设计和实现 hashCode() 方法。同时，为了保证对象的正确性和一致性，我们还需要实现 equals() 方法，并遵循相应的规范和原则。

综上所述，equals() 和 hashCode() 两个方法在 Java 中都具有重要的作用和意义，都不可或缺，不能只实现其中一个。同时使用 equals() 和 hashCode() 方法可以保证对象的正确性和一致性，并提供高效的对象比较和散列表查找功能。

**那为什么两个对象有相同的 hashCode 值，它们也不一定是相等的？**

在 Java 中，两个对象的哈希码相等，不一定意味着这两个对象相等。

首先，由于哈希码是一个有限的整数集合，它的取值范围相对较小，而 Java 中的对象数量通常较大，因此不同的对象可能会产生相同的哈希码。这种情况称为哈希冲突。

其次，即使两个对象的哈希码相等，它们也可能具有不同的内部状态、属性和字段，因此它们仍然可以是不同的对象。例如，对于一个 Person 类，如果我们只通过姓名来计算 hashCode 值，那么任何两个名字相同的 Person 对象的 hashCode 值都会相等。但是它们的年龄、性别、身高等其他属性可能各不相同，因此它们仍然可以是不同的对象。

综上所述，虽然两个对象的 hashCode 值相等时，它们可能代表相同的对象，但这并不是必然的关系。 在实际应用中，我们需要同时使用 equals() 和 hashCode() 方法，在遵循相应规范和原则的基础上，确保对象的正确性和一致性。

## 为什么重写 equals() 时必须重写 hashCode() 方法？

在 Java 中，重写 equals() 方法时通常也需要重写 hashCode() 方法。这是因为在使用散列表等数据结构时，对象的 hashCode 值通常会被用作该对象在哈希表中的索引位置。如果两个对象的 equals() 方法返回 true，但它们的 hashCode() 返回的值不同，那么它们就会被存储在哈希表的不同位置，从而导致哈希表的查找逻辑出现问题。

因此，为了确保对象的正确性和一致性，在重写 equals() 方法的同时，我们通常还需要重写 hashCode() 方法，并遵循如下规则：

1. 如果两个对象相等，则它们的 hashCode() 方法必须返回相同的值。

2. 如果两个对象不相等，则它们的 hashCode() 方法没有要求返回不同的值，但是为了提高散列表等数据结构的效率和减少冲突，不同对象的 hashCode 值应该尽可能不同。

在实际实现中，hashCode() 方法通常根据对象的属性值和字段值计算出一个哈希码。对于一些基本类型的属性，可以直接使用 Java 中的 hashCode() 方法进行计算；对于自定义类型的属性，可以递归调用该属性的 hashCode() 方法生成哈希码；对于数组类型的属性，可以使用 Arrays.hashCode() 方法进行计算。

综上所述，重写 equals() 方法时通常需要同时重写 hashCode() 方法，并遵循相关规范和原则，确保对象的正确性、一致性和优秀的哈希表性能。

# String

## String、StringBuffer、StringBuilder 的区别？

在 Java 中，String、StringBuffer 和 StringBuilder 都是字符串类型，但它们有一些区别。

1. String 类型是不可变的（immutable），即一旦创建就不能再修改其值。当对一个 String 对象进行拼接、替换、删除等操作时，实际上是创建了一个新的 String 对象，而原来的对象并没有发生改变。

2. StringBuffer 和 StringBuilder 类型是可变的（mutable），即可以对其值进行增加、删除、替换等操作，而且这些操作不会创建新的对象，而是在原来的对象中直接修改。

3. StringBuffer 和 StringBuilder 类型的区别在于线程安全性上。StringBuffer 是线程安全的，而 StringBuilder 不是。当多个线程同时对一个 StringBuffer 对象进行操作时，JVM 会进行同步处理，保证线程安全。而对于 StringBuilder 来说，如果多个线程同时对一个对象进行操作，就可能会导致数据不一致的问题。

推荐使用场景：

1. 如果需要频繁进行字符串拼接操作，并且在多线程环境中使用，建议使用 StringBuffer，因为它是线程安全的。

2. 如果需要频繁进行字符串拼接操作，并且在单线程环境中使用，建议使用 StringBuilder，因为它比 StringBuffer 更加高效。

3. 如果只需要对字符串进行读取和不可修改的操作，建议使用 String 类型，因为它更为简单、安全，并且具备优秀的性能表现。

综上所述，String、StringBuffer 和 StringBuilder 都是常用的字符串类型，在不同的应用场景中有着各自的优缺点和适用范围。

## String 为什么是不可变的?

在 Java 中，String 是一个不可变的对象，在创建后其值就不能被修改。这是因为 String 类型的设计，符合 Java 的安全性和性能要求，并带来了以下几个好处：

1. 线程安全：由于 String 对象是不可变的，所以多个线程可以共享同一个 String 对象，而无需进行额外的同步处理，从而提高了程序的并发性能。

2. 安全性：如果 String 对象是可变的，那么在传递参数、引用等操作时，可能会被意外地改变，从而导致问题和安全漏洞。而不可变的 String 对象可以避免这些问题的发生。

3. 哈希表优化：由于 String 不可变，所以它的哈希码只需要计算一次。在需要将 String 对象放入哈希表等数据结构中时，可以大大提高效率。

4. 字符串缓存池：由于 String 对象是不可变的，可以将一些常用的字符串对象缓存起来，以便在程序中重复使用，从而节约内存空间。

综上所述，String 对象不可变带来了许多优点。虽然它们也有一些限制，比如每次对 String 进行修改时必须创建一个新的 String 对象，但这些限制在大多数情况下都不会成为问题，反而可以提高代码的可维护性和安全性。

## 字符串拼接用“+” 还是 StringBuilder?

在 Java 中，字符串的拼接可以使用"+"符号或StringBuilder两种方式进行。对于少量的字符串拼接，使用"+"也是可以的，但对于大量的字符串拼接，使用StringBuilder更为高效。

在使用"+"符号进行字符串拼接时，每次操作都会创建一个新的String对象，并将原先的字符串和新的字符串进行拼接，如果这个操作频繁执行，就会产生大量的临时对象，从而导致内存消耗增加，程序性能下降。

而使用StringBuilder进行字符串拼接时，不会创建很多临时对象，而是通过在原始字符序列中修改、添加和删除字符实现字符串的操作。由于 StringBuilder 对象的长度是可变的，所以它避免了频繁创建和销毁对象的开销，从而提高了程序的性能。

需要注意的是，虽然 StringBuilder 是线程安全的，但在多线程环境中，它可能会出现竞态条件（race condition）等问题，因此建议在多线程环境中使用线程安全的 StringBuffer。

综上所述，对于大量的字符串拼接操作，推荐使用 StringBuilder，因为它比简单的字符串拼接操作更为高效，而且在一定程度上可以提高程序性能和效率。

## String#equals() 和 Object#equals() 有何区别？

在 Java 中，Object 类中提供了一个 equals() 方法用于判断两个对象是否相等。而在 String 类中，也提供了一个 equals() 方法，用于比较两个字符串是否相等。虽然这两个方法都用于判断对象是否相等，但它们之间存在一些区别。

1.参数类型不同：Object 类中的 equals() 方法比较的是两个对象是否引用同一个内存地址，而 String 类中的 equals() 方法比较的是两个字符串的值是否相等。

2.返回结果不同：Object 类中的 equals() 方法返回一个布尔值，表示两个对象是否相等。而 String 类中的 equals() 方法也返回一个布尔值，但是对于两个为 null 的字符串，String 类中的 equals() 方法返回 false，而 Object 类中的 equals() 方法则返回 true。

3.重写方式不同：由于 String 类中的 equals() 方法比较的是字符串的值，因此它需要进行字符串的比较操作。这个比较操作会先判断两个字符串是否具有相同的字符序列和长度，以及字符顺序是否相同，如果这些条件都满足，那么就认为两个字符串相等。与此不同的是，Object 类中的 equals() 方法需要进行对象的引用比较，因此它直接使用"=="运算符实现。

总之，String 类中的 equals() 方法与 Object 类中的 equals() 方法有所不同，前者比较的是字符串的值，后者比较的是对象的引用。在实际编程中，如果需要比较字符串是否相等，应该使用 String 类中的 equals() 方法，而不是使用 Object 类中的equals()方法。

## 字符串常量池的作用了解吗？

在 Java 中，字符串常量池是一个存储字符串的区域，在编译 Java 程序时，所有出现的字符串字面值都会被放到这个池中。如果在运行时需要创建相同的字符串对象，可以直接从字符串常量池中取得，而无需重新创建。

字符串常量池的作用主要有以下几点：

1. 节省内存：由于字符串常量池中的字符串对象是共享的，因此当多个字符串具有相同的内容时，它们可以共享同一个对象，从而避免了大量重复的字符串对象的创建，节省了内存空间。

2. 提高性能：由于字符串常量池中的字符串对象是共享的，因此可以直接使用"=="运算符比较两个字符串的引用是否相等。这比使用.equals()方法进行字符串比较更为高效，因为字符串比较操作是一项相对昂贵的操作。

3. 字符串缓存：很多库和框架都会使用字符串常量池来缓存字符串对象，以便在程序中进行重复使用。特别是在一些需要频繁使用字符串的场景下，使用字符串常量池可以大大提高程序的性能。

综上所述，字符串常量池是 Java 中一个非常重要的机制，它可以节省内存空间，提高程序执行效率，同时还可以提供字符串缓存功能，方便程序进行重复使用。

## String s1 = new String("abc");这句话创建了几个字符串对象？

在执行 String s1 = new String("abc"); 这条语句时，会创建两个字符串对象。

首先，由于字符串常量池中没有"abc"这个字符串常量，因此会在堆内存中创建一个新的字符串对象，其值为"abc"。这个字符串对象是通过 String 类的构造方法创建的，即 new String("abc")。

其次，由于使用了 new 关键字，会在堆内存中再创建一个新的字符串对象，也就是 s1 引用指向的对象。这个对象是通过 new 操作符创建的，并且它保存了对前面创建的字符串对象的引用。

因此，总共会创建两个字符串对象，一个位于字符串常量池中，一个位于堆内存中。需要注意的是，由于字符串常量池中的字符串对象是共享的，因此如果后续还有其他字符串对象需要使用"abc"这个字符串，都可以直接引用常量池中的那个对象，而无需重新创建。

## String#intern 方法有什么作用?

String#intern() 方法的作用是将一个字符串添加到字符串常量池中，并且返回字符串常量池中该字符串的引用。如果字符串常量池中已经存在该字符串，则直接返回字符串常量池中对应字符串的引用。

具体来说，当调用 s.intern() 方法时，系统会检查字符串常量池中是否已经有值为 s 的字符串对象。如果有，那么就返回该字符串对象的引用；如果没有，那么就将 s 对象添加到字符串常量池中，并返回该字符串对象的引用。

这个方法可以用于优化字符串的内存使用，特别是字符串对象需要频繁创建的场景下。由于字符串常量池中的对象是共享的，因此可以避免重复创建相同的字符串对象。这样，在程序执行期间，即使创建了多个相同的字符串对象，只要调用 intern() 方法将其添加到字符串常量池中，就可以避免对内存的浪费。

需要注意的是，由于字符串常量池是一个全局的区域，因此在程序中过度使用 inter() 方法，可能会导致字符串常量池中出现大量的字符串对象，从而占用大量的内存空间。因此，在使用 inter() 方法时，需要根据实际情况进行适当的判断和优化。

## String 类型的变量和常量做“+”运算时发生了什么？

在 Java 中，字符串变量和常量做"+"运算时会调用 String 类的 concat() 方法进行字符串拼接。具体来说，如果 a 和 b 是两个字符串变量或常量，则表达式 a + b 的执行过程如下：

1. 首先创建一个 StringBuilder 对象，用于存储合并后的字符串。StringBuilder 是 Java 中一个可变的字符序列类，可以高效地进行字符串拼接操作。

2. 然后将 a 中的内容添加到 StringBuilder 对象中。

3. 最后将 b 中的内容添加到 StringBuilder 对象中，并返回最终结果（也就是合并后的字符串）。

需要注意的是，由于字符串在 Java 中是不可修改的，因此每次对字符串进行修改（包括拼接）时都会创建一个新的字符串对象。因此，在对长字符串进行频繁的拼接操作时，为了避免大量的对象创建和内存消耗，推荐使用 StringBuilder 或 StringBuffer 来完成字符串的拼接操作。

另外，如果字符串变量和常量采用"="赋值运算符连接，如 String str = "hello " + "world"; 此时编译器会将"hello world"优化为一个字符串，直接使用该字符串常量池中的对象来赋值给 str。所以这种情况是不会调用 concat() 方法的。



