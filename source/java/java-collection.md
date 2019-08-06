## java集合

### List 和 Set 区别

 
  List 是可重复集合，Set 是不可重复集合，这两个接口都实现了 Collection 父接口。
  

### List 和 Map 区别


  Map 未继承 Collection，而是独立的接口，Map 是一种把键对象和值对象进行映射的集合，它的每一个元素都包含了一对键对象和值对象，Map 中存储的数据是没有顺序的， 其 key 是不能重复的，它的值是可以有重复的。


### Arraylist 与 LinkedList 区别


  ArrayList 和 Vector 内部是线性动态数组结构，在查询效率上会高很多，Vector 是线程安全的，相比 ArrayList 线程不安全的，性能会稍慢一些。


### ArrayList 与 Vector 区别


  LinkedList：是双向链表的数据结构存储数据，在做查询时会按照序号索引数据进行前向或后向遍历，查询效率偏低，但插入数据时只需要记录本项的前后项即可，所以插入速度较快


### HashMap 和 Hashtable 的区别


  Hashtable：内部存储的键值对是无序的是按照哈希算法进行排序，与 HashMap 最大的区别就是线程安全。键或者值不能为 null，为 null 就会抛出空指针异常。


### HashSet 和 HashMap 区别

#### HashSet：
  　　HashSet实现了Set接口，它不允许集合中出现重复元素。当我们提到HashSet时，第一件事就是在将对象存储在
  HashSet之前，要确保重写hashCode（）方法和equals（）方法，这样才能比较对象的值是否相等，确保集合中没有
  储存相同的对象。如果不重写上述两个方法，那么将使用下面方法默认实现：
  	public boolean add(Object obj)方法用在Set添加元素时，如果元素值重复时返回 "false"，如果添加成功则返回"true"
  	
#### HashMap：
  　　HashMap实现了Map接口，Map接口对键值对进行映射。Map中不允许出现重复的键（Key）。Map接口有两个基本的实现TreeMap和HashMap。TreeMap保存了对象的排列次序，而HashMap不能。HashMap可以有空的键值对（Key（null）-Value（null））
  HashMap是非线程安全的（非Synchronize），要想实现线程安全，那么需要调用collections类的静态方法synchronizeMap（）实现。
  public Object put(Object Key,Object value)方法用来将元素添加到map中。
  
#### HashSet与HashMap的区别：
  
  HashMap	HashSet
  实现了Map接口	实现Set接口
  存储键值对	仅存储对象
  调用put（）向map中添加元素	调用add（）方法向Set中添加元素
  HashMap使用键（Key）计算Hashcode	
  HashSet使用成员对象来计算hashcode值，
  对于两个对象来说hashcode可能相同，
  所以equals()方法用来判断对象的相等性，
  如果两个对象不同的话，那么返回false
  HashMap相对于HashSet较快，因为它是使用唯一的键获取对象	HashSet较HashMap来说比较慢
   
#### HashMap 的工作原理及代码实现


  1. 什么时候会使用HashMap？他有什么特点？
  是基于Map接口的实现，存储键值对时，它可以接收null的键值，是非同步的，HashMap存储着Entry(hash, key, value, next)对象。
  
  2. 你知道HashMap的工作原理吗？
  通过hash的方法，通过put和get存储和获取对象。存储对象时，我们将K/V传给put方法时，它调用hashCode计算hash从而得到bucket位置，进一步存储，HashMap会根据当前bucket的占用情况自动调整容量(超过Load Facotr则resize为原来的2倍)。获取对象时，我们将K传给get，它调用hashCode计算hash从而得到bucket位置，并进一步调用equals()方法确定键值对。如果发生碰撞的时候，Hashmap通过链表将产生碰撞冲突的元素组织起来，在Java 8中，如果一个bucket中碰撞冲突的元素超过某个限制(默认是8)，则使用红黑树来替换链表，从而提高速度。
  
  3. 你知道get和put的原理吗？equals()和hashCode()的都有什么作用？
  通过对key的hashCode()进行hashing，并计算下标( n-1 & hash)，从而获得buckets的位置。如果产生碰撞，则利用key.equals()方法去链表或树中去查找对应的节点
  
  4. 你知道hash的实现吗？为什么要这样实现？
  在Java 1.8的实现中，是通过hashCode()的高16位异或低16位实现的：(h = k.hashCode()) ^ (h >>> 16)，主要是从速度、功效、质量来考虑的，这么做可以在bucket的n比较小的时候，也能保证考虑到高低bit都参与到hash的计算中，同时不会有太大的开销。
  
  5. 如果HashMap的大小超过了负载因子(load factor)定义的容量，怎么办？
  如果超过了负载因子(默认0.75)，则会重新resize一个原来长度两倍的HashMap，并且重新调用hash方法。


### HashMap 和 ConcurrentHashMap 的区别


  引入ConcurrentHashMap是为了在同步集合HashTable之间有更好的选择，HashTable与HashMap、ConcurrentHashMap主要的区别在于HashMap不是同步的、线程不安全的和不适合应用于多线程并发环境下，而ConcurrentHashMap是线程安全的集合容器，特别是在多线程和并发环境中，通常作为Map的主要实现。除了线程安全外，他们之间还有一些细微的不同，本文会介绍到。顺便说说，HashMap和ConcurrentHashMap还有ConcurrentHashMap和Hashtable两者之间的区别在Java面试中经常出现，特别是高级Java程序员。
  HashMap与ConcurrentHashMap的区别
  在这部分，我们会看到更多关于HashMap和ConcurrentHashMap的细节和对比它们之间的参数比如线程安全、同步、性能和基本的使用。
  
  就像上面所说他们之间的第一个重要的区别就是ConcurrentHashMap是线程安全的和在并发环境下不需要加额外的同步。虽然它不像Hashtable那样需要同样的同步等级(全表锁)，但也有很多实际的用途。
  你可以使用Collections.synchronizedMap(HashMap)来包装HashMap作为同步容器，这时它的作用几乎与Hashtable一样,当每次对Map做修改操作的时候都会锁住这个Map对象，而ConcurrentHashMap会基于并发的等级来划分整个Map来达到线程安全，它只会锁操作的那一段数据而不是整个Map都上锁。
  
  ConcurrentHashMap有很好的扩展性，在多线程环境下性能方面比做了同步的HashMap要好，但是在单线程环境下，HashMap会比ConcurrentHashMap好一点。
  
  总结一下以上两者的区别，它们在线程安全、扩展性、同步之间的区别。如果是用于缓存的话，ConcurrentHashMap是一个更好的选择，在Java应用中会经常用到。ConcurrentHashMap在读操作线程数多于写操作线程数的情况下更胜一筹。
  ConcurrentHashMap vs Hashtable vs Synchronized Map
  虽然三个集合类在多线程并发应用中都是线程安全的，但是他们有一个重大的差别，就是他们各自实现线程安全的方式。Hashtable是jdk1的一个遗弃的类，它把所有方法都加上synchronized关键字来实现线程安全。所有的方法都同步这样造成多个线程访问效率特别低。Synchronized Map与HashTable差别不大，也是在并发中作类似的操作，两者的唯一区别就是Synchronized Map没被遗弃，它可以通过使用Collections.synchronizedMap()来包装Map作为同步容器使用。
  另一方面，ConcurrentHashMap的设计有点特别，表现在多个线程操作上。它不用做外的同步的情况下默认同时允许16个线程读和写这个Map容器。因为其内部的实现剥夺了锁，使它有很好的扩展性。不像HashTable和Synchronized Map，ConcurrentHashMap不需要锁整个Map，相反它划分了多个段(segments)，要操作哪一段才上锁那段数据。
  坦白说，集合类是一个最重要的Java API，我觉得恰当的使用它们是一种艺术。依我个人经验，我会使用ArrayList这些容器来提高自己的Java程序的性能，而不会去用一些遗弃的容器比如Vector等等，在Java 5之前，Java集合容器有一个很致命的缺陷就是缺乏可扩展性。
  同步集合类比如Hashtable和Vector在多线程Java应用里面逐渐成为障碍物；在jdk5后出现一些很好的并发集合，对大容量、低延迟的电子交易系统有很大影响，是快速存取数据的支柱
  
  ConcurrentHashMap 是一个并发散列映射表的实现，它允许完全并发的读取，并且支持给定数量的并发更新。相比于 HashTable 和用同步包装器包装的 HashMap（Collections.synchronizedMap(new HashMap())），ConcurrentHashMap 拥有更高的并发性。在 HashTable 和由同步包装器包装的 HashMap 中，使用一个全局的锁来同步不同线程间的并发访问。同一时间点，只能有一个线程持有锁，也就是说在同一时间点，只能有一个线程能访问容器。这虽然保证多线程间的安全并发访问，但同时也导致对容器的访问变成串行化的了。
  
  在使用锁来协调多线程间并发访问的模式下，减小对锁的竞争可以有效提高并发性。有两种方式可以减小对锁的竞争：
  
  减小请求 同一个锁的 频率。
  减少持有锁的 时间。
  ConcurrentHashMap 的高并发性主要来自于三个方面：
  
  用分离锁实现多个线程间的更深层次的共享访问。
  用 HashEntery 对象的不变性来降低执行读操作的线程在遍历链表期间对加锁的需求。
  通过对同一个 Volatile 变量的写 / 读访问，协调不同线程间读 / 写操作的内存可见性。
  使用分离锁，减小了请求 同一个锁的频率。
  
  通过 HashEntery 对象的不变性及对同一个 Volatile 变量的读 / 写来协调内存可见性，使得 读操作大多数时候不需要加锁就能成功获取到需要的值。由于散列映射表在实际应用中大多数操作都是成功的 读操作，所以 2 和 3 既可以减少请求同一个锁的频率，也可以有效减少持有锁的时间。
  
  通过减小请求同一个锁的频率和尽量减少持有锁的时间 ，使得 ConcurrentHashMap 的并发性相对于 HashTable 和用同步包装器包装的 HashMap有了质的提高




### ConcurrentHashMap 的工作原理及代码实现


  JDK 1.8中ConcurrentHashMap抛弃了分段锁技术的实现，直接采用CAS + synchronized保证并发更新的安全性，底层采用数组+链表+红黑树的存储结构。其包含核心静态内部类 Node。


  其实可以看出JDK1.8版本的ConcurrentHashMap的数据结构已经接近HashMap，相对而言，ConcurrentHashMap只是增加了同步的操作来控制并发，从JDK1.7    版本的ReentrantLock+Segment+HashEntry，到JDK1.8版本中synchronized+CAS+HashEntry+红黑树,相对而言，总结如下思考
  
  JDK1.8的实现降低锁的粒度，JDK1.7版本锁的粒度是基于Segment的，包含多个HashEntry，而JDK1.8锁的粒度就是HashEntry（首节点）
  JDK1.8版本的数据结构变得更加简单，使得操作也更加清晰流畅，因为已经使用synchronized来进行同步，所以不需要分段锁的概念，也就不需要Segment这种    数据结构了，由于粒度的降低，实现的复杂度也增加了
  JDK1.8使用红黑树来优化链表，基于长度很长的链表的遍历是一个很漫长的过程，而红黑树的遍历效率是很快的，代替一定阈值的链表，这样形成一个最佳拍档
  JDK1.8为什么使用内置锁synchronized来代替重入锁ReentrantLock，我觉得有以下几点
  因为粒度降低了，在相对而言的低粒度加锁方式，synchronized并不比ReentrantLock差，在粗粒度加锁中ReentrantLock可能通过Condition来控制各个低粒    度的边界，更加的灵活，而在低粒度中，Condition的优势就没有了
  JVM的开发团队从来都没有放弃synchronized，而且基于JVM的synchronized优化空间更大，使用内嵌的关键字比使用API更加自然
  在大量的数据操作下，对于JVM的内存压力，基于API的ReentrantLock会开销更多的内存，虽然不是瓶颈，但是也是一个选择依据


### ConcurrentHashMap原理分析（1.7与1.8）

   [ConcurrentHashMap原理分析（1.7与1.8）](https://www.cnblogs.com/study-everyday/p/6430462.html)

