## JVM十问

###  **Q1：JVM管理的内存结构是怎样的？**

Java虚拟机在执行Java程序的过程中会把他所管理的内存划分为若干个不同的数据区域。《Java虚拟机规范》中规定了JVM所管理的内存需要包括一下几个运行时区域：

<img src="..\_static\jvm-1.webp" >

Java虚拟机运行时数据区域主要包含了PC寄存器（程序计数器）、Java虚拟机栈、本地方法栈、Java堆、方法区以及运行时常量池。

各个区域有各自不同的作用，关于各个区域的作用就不在本文中相信介绍了。

但是，需要注意的是，上面的区域划分只是逻辑区域，规范对于有些区域的限制是比较松的，所以不同的虚拟机厂商在实现上，甚至是同一款虚拟机的不同版本也是不尽相同的。



###  **Q2：不同的虚拟机在实现运行时内存的时候有什么区别？**

前面提到过《Java虚拟机规范》定义的JVM运行时所需的内存区域，不同的虚拟机实现上有所不同，而在这么多区域中，规范对于方法区的管理是最宽松的，规范中关于这部分的描述如下：

方法区在虚拟机启动的时候创建，虽然方法区是堆的逻辑组成部分，但是简单的虚拟机实现可以选择在这个区域不实现垃圾收集与压缩。本版本的规范也不限定实现方法区的内存位置和代码编译的管理策略。方法区的容量可以是固定的，也可以随着程序执行的需求动态扩展，并在不需要过多的空间时自行收缩。方法区在实际内存空间站可以是不连续的。

这一规定，可以说是给了虚拟机厂商很大的自由。

虚拟机规范对方法区实现的位置并没有明确要求，在最著名的HotSopt虚拟机实现中（在Java 8 之前），方法区仅是逻辑上的独立区域，在物理上并没有独立于堆而存在，而是位于永久代中。所以，这时候方法区也是可以被垃圾回收的。

实践证明，JVM中存在着大量的声明短暂的对象，还有一些生命周期比较长的对象。为了对他们采用不同的收集策略，采用了分代收集算法，所以HotSpot虚拟机把的根据对象的年龄不同，把堆分位新生代、老年代和永久代。

在Java 8中 ，HotSpot虚拟机移除了永久代，使用本地内存来存储类元数据信息并称之为：元空间（Metaspace）

<img src="..\_static\jvm-2.webp" >

￼



###  **Q3：运行时数据区中哪些区域是线程共享的？哪些是独享的？**

在JVM运行时内存区域中，PC寄存器、虚拟机栈和本地方法栈是线程独享的。

而Java堆、方法区是线程共享的。但是值得注意的是，Java堆其实还未每一个线程单独分配了一块[TLAB](http://mp.weixin.qq.com/s?__biz=MzI3NzE0NjcwMg==&mid=2650124457&idx=1&sn=1c33947700dfb28048df4a913b434077&chksm=f36bad88c41c249ea854b371a1c8597959e2e35c2890bdd6a5945df0b568bdfc980d1dd2cf2b&scene=21#wechat_redirect)空间，这部分空间在分配时是线程独享的，在使用时是线程共享的。（[TLAB介绍](http://mp.weixin.qq.com/s?__biz=MzI3NzE0NjcwMg==&mid=2650124457&idx=1&sn=1c33947700dfb28048df4a913b434077&chksm=f36bad88c41c249ea854b371a1c8597959e2e35c2890bdd6a5945df0b568bdfc980d1dd2cf2b&scene=21#wechat_redirect)）



###  **Q4：除了JVM运行时内存以外，还有什么区域可以用吗？**

除了我们前面介绍的虚拟机运行时数据区以外，还有一部分内存也被频繁使用，他不是运行时数据区的一部分，也不是Java虚拟机规范中定义的内存区域，他就是——直接内存。

直接内存的分配不受Java堆大小的限制，但是他还是会收到服务器总内存的影响。

在JDK 1.4中引入的NIO中，引入了一种基于Channel和Buffer的I/O方式，他可以使用Native函数直接分配堆外内存，然后通过一个存储在Java堆中的DirectByteBuffer对象作为这块内存的应用进行操作。

<img src="..\_static\jvm-3.webp" >

￼

###  **Q5：堆和栈的区别是什么？**

堆和栈（虚拟机栈）是完全不同的两块内存区域，一个是线程独享的，一个是线程共享的，二者之间最大的区别就是存储的内容不同：

堆中主要存放对象实例。 
栈（局部变量表）中主要存放各种基本数据类型、对象的引用。



###  **Q6：Java中的数组是存储在堆上还是栈上的？**

在Java中，数组同样是一个对象，所以对象在内存中如何存放同样适用于数组；

所以，数组的实例是保存在堆中，而数组的引用是保存在栈上的。

<img src="..\_static\jvm-4.webp" >

￼

###  **Q7：Java中的对象创建有多少种方式？**

Java中共有5种方式可以创建一个对象。

最简单的方式就是使用new关键字。

```
User user = new User();
```

除此以外，还可以使用反射机制创建对象：

```
User user = User.class.newInstance();
```

或者使用Constructor类的newInstance：

```
Constructor&lt;User&gt; constructor = User.class.getConstructor();
User user = constructor.newInstance();
```

除此之外还可以使用clone方法和反序列化的方式，这两种方式不常用并且代码比较复杂，就不在这里展示了，感兴趣的可以自行了解下。



###  **Q8：Java中对象创建的过程是怎么样的？**

对于一个普通的Java对象的创建，大致过程如下：

1、虚拟机遇到new指令，到常量池定位到这个类的符号引用。 
2、检查符号引用代表的类是否被加载、解析、初始化过。 
3、虚拟机为对象分配内存。 
4、虚拟机将分配到的内存空间都初始化为零值。 
5、虚拟机对对象进行必要的设置。 
6、执行方法，成员变量进行初始化。



###  **Q9：Java中的对象一定在堆上分配内存吗？**

前面我们说过，Java堆中主要保存了对象实例，但是，随着JIT编译期的发展与[逃逸分析](http://mp.weixin.qq.com/s?__biz=MzI3NzE0NjcwMg==&mid=2650121615&idx=1&sn=00d412f68fe58dceab6d13fdfefac113&chksm=f36bb8aec41c31b8d62069e2663345c0452ebdded331616496637e19b2cad72725f6ce90daec&scene=21#wechat_redirect)技术逐渐成熟，[栈上分配](http://mp.weixin.qq.com/s?__biz=MzI3NzE0NjcwMg==&mid=2650121307&idx=1&sn=5526473d0248cca8385d2a18ba6b25af&chksm=f36bb97ac41c306c354ebf0335cd2fd77cac03f3434894e4e5b44a01754a5494b04350d26d14&scene=21#wechat_redirect)、标量替换优化技术将会导致一些微妙的变化，所有的对象都分配到堆上也渐渐变得不那么“绝对”了。

其实，在编译期间，JIT会对代码做很多优化。其中有一部分优化的目的就是减少内存堆分配压力，其中一种重要的技术叫做逃逸分析。

如果JIT经过逃逸分析，发现有些对象没有逃逸出方法，那么有可能堆内存分配会被优化成栈内存分配。（关于逃逸分析和栈上分配可以参考：[深入理解Java中的逃逸分析](http://mp.weixin.qq.com/s?__biz=MzI3NzE0NjcwMg==&mid=2650121615&idx=1&sn=00d412f68fe58dceab6d13fdfefac113&chksm=f36bb8aec41c31b8d62069e2663345c0452ebdded331616496637e19b2cad72725f6ce90daec&scene=21#wechat_redirect)、[对象并不一定都是在堆上分配内存的](http://mp.weixin.qq.com/s?__biz=MzI3NzE0NjcwMg==&mid=2650121307&idx=1&sn=5526473d0248cca8385d2a18ba6b25af&chksm=f36bb97ac41c306c354ebf0335cd2fd77cac03f3434894e4e5b44a01754a5494b04350d26d14&scene=21#wechat_redirect)）

<img src="..\_static\jvm-5.webp" >

￼

###  **Q10：怎么如何获取堆和栈的dump文件？**

Java Dump，Java虚拟机的运行时快照。将Java虚拟机运行时的状态和信息保存到文件。

可以使用在服务器上使用[jmap命令](http://mp.weixin.qq.com/s?__biz=MzI3NzE0NjcwMg==&mid=402312019&idx=1&sn=97736feb967ecbffb454fa037015ad6d&chksm=7964d6724e135f64a5c0d65e41afbeac45700dd91149375f99071731954e855e13b11cd6c30b&scene=21#wechat_redirect)来获取堆dump，使用[jstack命令](http://mp.weixin.qq.com/s?__biz=MzI3NzE0NjcwMg==&mid=402296484&idx=1&sn=8e7fc8197a216afb590b17e15f9b721e&chksm=796493854e131a932b3dd53839820eaba022cb87a601062b6bf6a574d742cd8e92a707432173&scene=21#wechat_redirect)来获取线程的调用栈dump。