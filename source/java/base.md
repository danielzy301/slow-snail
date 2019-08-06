## 基础篇

### 基本功

- 面向对象的特征

  ```java
  封装,继承，多态
  ```

- [Java](http://lib.csdn.net/base/17)四种引用包括强引用，软引用，弱引用，虚引用。

  ```
  ⑴强引用（StrongReference）
  强引用是使用最普遍的引用。如果一个对象具有强引用，那垃圾回收器绝不会回收它。当内存空间不足，Java虚拟机宁愿抛出OutOfMemoryError错误，使程序异常终止，也不会靠随意回收具有强引用的对象来解决内存不足的问题。  ps：强引用其实也就是我们平时A a = new A()这个意思。
  
  ⑵软引用（SoftReference）
  如果一个对象只具有软引用，则内存空间足够，垃圾回收器就不会回收它；如果内存空间不足了，就会回收这些对象的内存。只要垃圾回收器没有回收它，该对象就可以被程序使用。软引用可用来实现内存敏感的高速缓存（下文给出示例）。
  软引用可以和一个引用队列（ReferenceQueue）联合使用，如果软引用所引用的对象被垃圾回收器回收，Java虚拟机就会把这个软引用加入到与之关联的引用队列中。
  
  ⑶弱引用（WeakReference）
  弱引用与软引用的区别在于：只具有弱引用的对象拥有更短暂的生命周期。在垃圾回收器线程扫描它所管辖的内存区域的过程中，一旦发现了只具有弱引用的对象，不管当前内存空间足够与否，都会回收它的内存。不过，由于垃圾回收器是一个优先级很低的线程，因此不一定会很快发现那些只具有弱引用的对象。
  弱引用可以和一个引用队列（ReferenceQueue）联合使用，如果弱引用所引用的对象被垃圾回收，Java虚拟机就会把这个弱引用加入到与之关联的引用队列中。
  
  ⑷虚引用（PhantomReference）
  “虚引用”顾名思义，就是形同虚设，与其他几种引用都不同，虚引用并不会决定对象的生命周期。如果一个对象仅持有虚引用，那么它就和没有任何引用一样，在任何时候都可能被垃圾回收器回收。
  虚引用主要用来跟踪对象被垃圾回收器回收的活动。虚引用与软引用和弱引用的一个区别在于：虚引用必须和引用队列 （ReferenceQueue）联合使用。当垃圾回收器准备回收一个对象时，如果发现它还有虚引用，就会在回收对象的内存之前，把这个虚引用加入到与之 关联的引用队列中。
  ```

  

- Spring,Spring MVC及Spring Boot区别

  - 我们说到Spring，一般指代的是Spring Framework，它是一个开源的应用程序框架，提供了一个简易的开发方式，**通过这种开发方式，将避免那些可能致使代码变得繁杂混乱的大量的业务/工具对象，说的更通俗一点就是由框架来帮你管理这些对象，包括它的创建，销毁等**，比如基于Spring的项目里经常能看到的`Bean`，它代表的就是由Spring管辖的对象。

  - Spring 的核心功能远不知这些，如：

    - Spring AOP
    - Spring JDBC
    - Spring MVC
    - Spring ORM
    - Spring JMS
    - Spring Test

  - Spring MVC是Spring的一部分，Spring 出来以后，大家觉得很好用，于是按照这种模式设计了一个 MVC框架（一些用Spring 解耦的组件），**主要用于开发WEB应用和网络接口，它是Spring的一个模块，通过Dispatcher Servlet, ModelAndView 和 View Resolver，让应用开发变得很容易**

  - 初期的Spring通过代码加配置的形式为项目提供了良好的灵活性和扩展性，但随着Spring越来越庞大，其配置文件也越来越繁琐，太多复杂的xml文件也一直是Spring被人诟病的地方，特别是近些年其他简洁的WEB方案层出不穷，如基于Python或Node.Js，几行代码就能实现一个WEB服务器，对比起来，大家渐渐觉得Spring那一套太过繁琐，此时，Spring社区推出了Spring Boot，它的目的在于**实现自动配置，降低项目搭建的复杂度**，

  - ```
    spring-boot-starter-web-services，针对SOAP Web Services
    
    spring-boot-starter-web，针对Web应用与网络接口
    
    spring-boot-starter-jdbc，针对JDBC
    
    spring-boot-starter-data-jpa，基于hibernate的持久层框架
    
    spring-boot-starter-cache，针对缓存支持
    ```

  - 这三者专注的领域不同，解决的问题也不一样；总的来说，Spring 就像一个大家族，有众多衍生产品例如 Boot，Security，JPA等等。但他们的基础都是Spring 的 IOC 和 AOP，IOC提供了依赖注入的容器，而AOP解决了面向切面的编程，然后在此两者的基础上实现了其他衍生产品的高级功能；Spring MVC是基于 Servlet 的一个 MVC 框架，主要解决 WEB 开发的问题，因为 Spring 的配置非常复杂，各种xml，properties处理起来比较繁琐。于是为了简化开发者的使用，Spring社区创造性地推出了Spring Boot，它遵循约定优于配置，极大降低了Spring使用门槛，但又不失Spring原本灵活强大的功能

  

- final, finally, finalize 的区别

  ```java
  final:
  1. final修饰类的时，表明该类不能被其他类所继承
  2. 使用final方法的原因主要有两个:把方法锁定，以防止继承类对其进行更改,效率，在早期的java版本中，会将final方法转为内嵌调用.但若方法过于庞大，可能在性能上不会有多大提升。因此在最近版本中，不需要final方法进行这些优化了。
  3. final成员变量表示常量，只能被赋值一次，赋值后其值不再改变
  finally:
  finally作为异常处理的一部分，它只能用在try/catch语句中，并且附带一个语句块，表示这段语句最终一定会被执行（不管有没有抛出异常），经常被用在需要释放资源的情况下. 但当调用system.exit()时，finally不会被执行。
  finalize：
  finalize()是在java.lang.Object里定义的，也就是说每一个对象都有这么个方法。这个方法在gc启动，该对象被回收的时候被调用。特殊情况下，需要程序员实现finalize，当对象被回收的时候释放一些资源，比如：一个socket链接，在对象初始化时创建，整个生命周期内有效，那么就需要实现finalize，关闭这个链接。 
  　　使用finalize还需要注意一个事，调用super.finalize();
  　　一个对象的finalize()方法只会被调用一次，而且finalize()被调用不意味着gc会立即回收该对象，所以有可能调用finalize()后，该对象又不需要被回收了，然后到了真正要被回收的时候，因为前面调用过一次，所以不会调用finalize()，产生问题。 所以，推荐不要使用finalize()方法，它跟析构函数不一样。
  ```

- int 和 Integer 有什么区别

  ```java
  1、Integer是int的包装类，int则是java的一种基本数据类型 
  2、Integer变量必须实例化后才能使用，而int变量不需要 
  3、Integer实际是对象的引用，当new一个Integer时，实际上是生成一个指针指向此对象；而int则是直接存储数据值 
  4、Integer的默认值是null，int的默认值是0
  ```

- 重载和重写的区别

- 抽象类和接口有什么区别

- 说说反射的用途及实现

  ```java
  反射的核心：是 JVM 在运行时 才动态加载的类或调用方法或属性，他不需要事先（写代码的时候或编译期）知道运行对象是谁。
  Java反射框架提供以下功能:
  ①、在运行时判断任意一个对象所属的类
  ②、在运行时构造任意一个类的对象
  ③、在运行时判断任意一个类所具有的成员变量和方法（通过反射设置可以调用 private）
  ④、在运行时调用人一个对象的方法
  反射最重要的用途就是开发各种通用框架。
  ```

- 说说自定义注解的场景及实现

  ```
  跟踪代码的依赖性，实现代替配置文件的功能。比较常见的是Spring等框架中的基于注解配置。
  还可以生成文档常见的@See@param@return等。如@override放在方法签名，如果这个方法 并不是覆盖了超类方法，则编译时就能检查出。
  使用@interface自定义注解时，自动继承了java.lang.annotation.Annotation接口，由编译程序自动完成其他细节，在定义注解时，不能继承其他注解或接口。
  ```

- HTTP 请求的 GET 与 POST 方式的区别

  ```
  GET在浏览器回退时是无害的，而POST会再次提交请求。
  GET产生的URL地址可以被Bookmark，而POST不可以。
  GET请求会被浏览器主动cache，而POST不会，除非手动设置。
  GET请求只能进行url编码，而POST支持多种编码方式。
  GET请求参数会被完整保留在浏览器历史记录里，而POST中的参数不会被保留。
  GET请求在URL中传送的参数是有长度限制的，而POST么有。
  对参数的数据类型，GET只接受ASCII字符，而POST没有限制。
  GET比POST更不安全，因为参数直接暴露在URL上，所以不能用来传递敏感信息。
  GET参数通过URL传递，POST放在Request body中
  
  GET和POST是什么？HTTP协议中的两种发送请求的方法。
  HTTP是什么？HTTP是基于TCP/IP的关于数据如何在万维网中如何通信的协议。
  HTTP的底层是TCP/IP。所以GET和POST的底层也是TCP/IP，也就是说，GET/POST都是TCP链接。GET和POST能做的事情是一样一样的。你要给GET加上request body，给POST带上url参数，技术上是完全行的通的。 
  
  GET产生一个TCP数据包；POST产生两个TCP数据包。
  对于GET方式的请求，浏览器会把http header和data一并发送出去，服务器响应200（返回数据）；
  而对于POST，浏览器先发送header，服务器响应100 continue，浏览器再发送data，服务器响应200 ok（返回数据）。
  ```

- session 与 cookie 区别

  ```
  1、Cookie和Session都是会话技术，Cookie是运行在客户端，Session是运行在服务器端。
  2、Cookie有大小限制以及浏览器在存cookie的个数也有限制，Session是没有大小限制和服务器的内存大小有关。
  3、Cookie有安全隐患，通过拦截或本地文件找得到你的cookie后可以进行攻击。
  4、Session是保存在服务器端上会存在一段时间才会消失，如果session过多会增加服务器的压力。
  
  1、session是保存在服务器端，理论上是没有是没有限制，只要你的内存够大
  2、浏览器第一次访问服务器时会创建一个session对象并返回一个JSESSIONID=ID的值，
     创建一个Cookie对象key为JSSIONID，value为ID的值，将这个Cookie写回浏览器
  3、浏览器在第二次访问服务器的时候携带Cookie信息JSESSIONID=ID的值，如果该JSESSIONID的session已经销毁，那么会重新创建一个新的session再返回一个新的JSESSIONID通过Cookie返回到浏览器
  4、针对一个web项目，一个浏览器是共享一个session，就算有两个web项目部署在同一个服务器上，针对两个项目的session是不同的.如：你在tomcat上同时部署了两个web项目，分别是web1、web2。当你在一个浏览器上同时访问web1时创建的session是A1，访问web2时创建的session是A2。后面你再多次访问web1使用的session还是A1,多次访问web2时使用session就是A2
  5、session是基于Cookie技术实现，重启浏览器后再次访问原有的连接依然会创建一个新的session，因为Cookie在关闭浏览器后就会消失，但是原来服务器的Session还在，只有等到了销毁的时间会自动销毁
  6、如果浏览器端禁用了Cookie，那么每次访问都会创建一个新的Session，但是我们可以通过服务器端程序重写URL即可，如果页面多连接多，会增加不必要的工作量，
  ```

- session 分布式处理

  ```
  第一种：粘性session
  原理：粘性Session是指将用户锁定到某一个服务器上，比如上面说的例子，用户第一次请求时，负载均衡器将用户的请求转发到了A服务器上，如果负载均衡器设置了粘性Session的话，那么用户以后的每次请求都会转发到A服务器上，相当于把用户和A服务器粘到了一块，这就是粘性Session机制。
  优点：简单，不需要对session做任何处理。
  缺点：缺乏容错性，如果当前访问的服务器发生故障，用户被转移到第二个服务器上时，他的session信息都将失效。
  适用场景：发生故障对客户产生的影响较小；服务器发生故障是低概率事件。
  实现方式：以Nginx为例，在upstream模块配置ip_hash属性即可实现粘性Session。
  第二种：服务器session复制
  原理：任何一个服务器上的session发生改变（增删改），该节点会把这个 session的所有内容序列化，然后广播给所有其它节点，不管其他服务器需不需要session，以此来保证Session同步。
  优点：可容错，各个服务器间session能够实时响应。
  缺点：会对网络负荷造成一定压力，如果session量大的话可能会造成网络堵塞，拖慢服务器性能。
  第三种：session共享机制
  使用分布式缓存方案比如memcached、redis，但是要求Memcached或Redis必须是集群。
  第四种：session持久化到数据库
  原理：就不用多说了吧，拿出一个数据库，专门用来存储session信息。保证session的持久化。
  优点：服务器出现问题，session不会丢失
  缺点：如果网站的访问量很大，把session存储到数据库中，会对数据库造成很大压力，还需要增加额外的开销维护数据库
  第五种terracotta实现session复制
  原理：Terracotta的基本原理是对于集群间共享的数据，当在一个节点发生变化的时候，Terracotta只把变化的部分发送给Terracotta服务器，然后由服务器把它转发给真正需要这个数据的节点。可以看成是对第二种方案的优化。
  优点：这样对网络的压力就非常小，各个节点也不必浪费CPU时间和内存进行大量的序列化操作。把这种集群间数据共享的机制应用在session同步上，既避免了对数据库的依赖，又能达到负载均衡和灾难恢复的效果。
  ```

- JDBC 流程

  ```
  JDBC：Java Data Base Connection
  JDBC是用于运行sql语句并从数据库中获取新新的java API.
  JDBC是用来（让我们的程序）通过网络来操作数据库的，作用非常重要；JDBC技术也是Java核心技术之中的一个。
  通过JDBC操作数据库——步骤
  　  第1步：注冊驱动 (仅仅做一次)
  　　第2步：建立连接(Connection)
  　　第3步：创建运行SQL的语句(Statement)
  　　第4步：运行语句
  　　第5步：处理运行结果(ResultSet)
  　　第6步：释放资源
  
  Java中的JDBC驱动可以分为四种类型，包括JDBC-ODBC桥、本地API驱动、网络协议驱动和本地协议驱动。
  	 JDBC驱动类型一、JDBC-ODBC 桥 是sun公司提供的，是jdk提供的的标准API. 这种类型的驱动实际是把所有 JDBC的调用传递给ODBC ,再由ODBC调用本地数据库驱动代码.
     JDBC驱动类型二、本地API驱动直接把JDBC调用转变为数据库的标准调用再去访问数据库.
  这种方法需要本地 数据库驱动代码. 本地API驱动 | 厂商DB代码---------------数据库Server (图二) 这种驱动比起JDBC-ODBC桥执行效率大大提高了.但是,它仍然需要在客户端加载数据库厂商 提供的代码库.这样就不适合基于internet的应用.并且,他的执行效率比起3,4型的JDBC驱动 还是不够高.
  	JDBC驱动类型三、网络协议驱动
  这种驱动实际上是根据我们熟悉的三层结构建立的. JDBC先把对数局库的访问请求传递给网 络上的中间件服务器. 中间件服务器再把请求翻译为符合数据库规范的调用,再把这种调用 传给数据库服务器.如果中间件服务器也是用java开法的,那么在在中间层也可以使用1,2型 JDBC驱动程序作为访问数据库的方法. 网络协议驱动---------中间件服务器------------数据库Server
  由于这种驱动是基于server的.所以,它不需要在客户端加载数据库厂商提供的代码库.而且 他在执行效率和可升级性方面是比较好的.因为大部分功能实现都在server端,所以这种驱动 可以设计的很小,可以非常快速的加载到内存中. 但是,这种驱动在中间件层仍然需要有配置 其它数据库驱动程序,并且由于多了一个中间层传递数据,它的执行效率还不是最好.
  	JDBC驱动类型四、本地协议驱动
  这种驱动直接把JDBC调用转换为符合相关数据库系统规范的请求.由于4型驱动写的应用可 以直接和数据库服务器通讯.这种类型的驱动完全由java实现,因此实现了平台独立性. 本地协议驱动---------数据库Server
  由于这种驱动不需要先把JDBC的调用传给ODBC或本地数据库接口或者是中间层服务器.所 以它的执行效率是非常高的.而且,它根本不需要在客户端或服务器端装载任何的软件或驱动. 这种驱动程序可以动态的被下载.但是对于不同的数据库需要下载不同的驱动程序.
  ```

- Druid 数据库连接池技术

  ```
  Druid首先是一个数据库连接池。Druid是目前最好的数据库连接池，在功能、性能、扩展性方面，都超过其他数据库连接池，包括DBCP、C3P0、BoneCP、Proxool、JBoss DataSource。Druid是阿里巴巴开发的号称为监控而生的数据库连接池！
  功能：
  1、替换DBCP和C3P0。Druid提供了一个高效、功能强大、可扩展性好的数据库连接池。
  2、可以监控数据库访问性能，Druid内置提供了一个功能强大的StatFilter插件，能够详细统计SQL的执行性能，这对于线上分析数据库访问性能有帮助。
  3、数据库密码加密。直接把数据库密码写在配置文件中，这是不好的行为，容易导致安全问题。DruidDruiver和DruidDataSource都支持PasswordCallback。
  4、SQL执行日志，Druid提供了不同的LogFilter，能够支持Common-Logging、Log4j和JdkLog，你可以按需要选择相应的LogFilter，监控你应用的数据库访问情况。
  5、扩展JDBC，如果你要对JDBC层有编程的需求，可以通过Druid提供的Filter机制，很方便编写JDBC层的扩展插件。
  所以Druid可以：
  1、充当数据库连接池。
  2、可以监控数据库访问性能
  3、获得SQL执行日志
  ```

- MVC 设计思想

- equals 与 == 的区别

### 集合

- List 和 Set 区别

  ```
  List 是可重复集合，Set 是不可重复集合，这两个接口都实现了 Collection 父接口。
  ```

- List 和 Map 区别

  ```
  Map 未继承 Collection，而是独立的接口，Map 是一种把键对象和值对象进行映射的集合，它的每一个元素都包含了一对键对象和值对象，Map 中存储的数据是没有顺序的， 其 key 是不能重复的，它的值是可以有重复的。
  ```

- Arraylist 与 LinkedList 区别

  ```
  ArrayList 和 Vector 内部是线性动态数组结构，在查询效率上会高很多，Vector 是线程安全的，相比 ArrayList 线程不安全的，性能会稍慢一些。
  ```

- ArrayList 与 Vector 区别

  ```
  LinkedList：是双向链表的数据结构存储数据，在做查询时会按照序号索引数据进行前向或后向遍历，查询效率偏低，但插入数据时只需要记录本项的前后项即可，所以插入速度较快
  ```

- HashMap 和 Hashtable 的区别

  ```
  Hashtable：内部存储的键值对是无序的是按照哈希算法进行排序，与 HashMap 最大的区别就是线程安全。键或者值不能为 null，为 null 就会抛出空指针异常。
  ```

- HashSet 和 HashMap 区别

  ```
  HashSet：
  　　HashSet实现了Set接口，它不允许集合中出现重复元素。当我们提到HashSet时，第一件事就是在将对象存储在
  HashSet之前，要确保重写hashCode（）方法和equals（）方法，这样才能比较对象的值是否相等，确保集合中没有
  储存相同的对象。如果不重写上述两个方法，那么将使用下面方法默认实现：
  	public boolean add(Object obj)方法用在Set添加元素时，如果元素值重复时返回 "false"，如果添加成功则返回"true"
  	
  HashMap：
  　　HashMap实现了Map接口，Map接口对键值对进行映射。Map中不允许出现重复的键（Key）。Map接口有两个基本的实现TreeMap和HashMap。TreeMap保存了对象的排列次序，而HashMap不能。HashMap可以有空的键值对（Key（null）-Value（null））
  HashMap是非线程安全的（非Synchronize），要想实现线程安全，那么需要调用collections类的静态方法synchronizeMap（）实现。
  public Object put(Object Key,Object value)方法用来将元素添加到map中。
  
  HashSet与HashMap的区别：
  
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
   
  ```

- HashMap 和 ConcurrentHashMap 的区别

  ```
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
  
  ##  ConcurrentHashMap 是一个并发散列映射表的实现，它允许完全并发的读取，并且支持给定数量的并发更新。相比于 HashTable 和用同步包装器包装的 HashMap（Collections.synchronizedMap(new HashMap())），ConcurrentHashMap 拥有更高的并发性。在 HashTable 和由同步包装器包装的 HashMap 中，使用一个全局的锁来同步不同线程间的并发访问。同一时间点，只能有一个线程持有锁，也就是说在同一时间点，只能有一个线程能访问容器。这虽然保证多线程间的安全并发访问，但同时也导致对容器的访问变成串行化的了。
  
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
  ```

- HashMap 的工作原理及代码实现

  ```
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
  ```

- ConcurrentHashMap 的工作原理及代码实现

  ```
  JDK 1.8中ConcurrentHashMap抛弃了分段锁技术的实现，直接采用CAS + synchronized保证并发更新的安全性，底层采用数组+链表+红黑树的存储结构。其包含核心静态内部类 Node。
  ```

  

### 线程

- 创建线程的方式及实现

  ```
  继承Thread类创建线程　
  1】d定义Thread类的子类，并重写该类的run()方法，该方法的方法体就是线程需要完成的任务，run()方法也称为线程执行体。
  2】创建Thread子类的实例，也就是创建了线程对象
  3】启动线程，即调用线程的start()方法
  
  实现Runnable接口创建线程
  1】定义Runnable接口的实现类，一样要重写run()方法，这个run（）方法和Thread中的run()方法一样是线程的执行体
  2】创建Runnable实现类的实例，并用这个实例作为Thread的target来创建Thread对象，这个Thread对象才是真正的线程对象
  3】第三部依然是通过调用线程对象的start()方法来启动线程
  
  使用Callable和Future创建线程
  1】创建Callable接口的实现类，并实现call()方法，然后创建该实现类的实例（从java8开始可以直接使用Lambda表达式创建Callable对象）。
  2】使用FutureTask类来包装Callable对象，该FutureTask对象封装了Callable对象的call()方法的返回值
  3】使用FutureTask对象作为Thread对象的target创建并启动线程（因为FutureTask实现了Runnable接口）
  4】调用FutureTask对象的get()方法来获得子线程执行结束后的返回值
  ```

- sleep() 、join（）、yield（）有什么区别

  ```
  1. sleep()方法
      在指定的毫秒数内让当前正在执行的线程休眠(暂停执行)。此操作受到系统计时器和调度程序精准和准确性的影响，让其他线程有机会继续执行，但是它不释放对象锁。也就是如果有synchronized同步块，其他线程仍然不能访问共享数据，注意该方法需要捕获异常。
      比如有两个线程同时执行(没有synchronized)，一个线程优先级为Max_PRIORITY，另一个为MIN_PRIORITY，如果没有sleep()方法，只有高的优先级的线程执行完成后，低优先级的线程才能执行；但当高优先级的线程sleep(5000)后，低优先级的就有机会执行了。
  总之，sleep()可以使用低优先级的线程得到执行的机会，当然也可以让同优先级的线程有执行的机会。
  
  2. yield()方法
      yield()方法和sleep()方法类似，也不会释放“锁标志”，区别在于，它没有参数，即yield()方法只是使当前线程重新回到可执行状态，所以执行yield()的线程有可能在进入到可执行状态后，马上又被执行，另外yield()方法只能使用同优先级或者高优先级的线程得到执行机会，这也和sleep()方法不同
  
  3. join()方法
      Thread的非静态方法join()让一个线程B“加入”到另一个线程A的尾部，在A执行完毕之前，B不能工作。
    Thread  t = new MyThread(); t.start(); t.jion();
  保证当前线程是停止执行的，直到该线程所加入的线程完成为止。然而，如果它加入的线程没有存活，则当前线程不需要停止。
  
  4. wait()方法
  在其他线程调用对象的notify或notifyAll方法前，导致当前线程等待。线程会释放掉它所占有的“锁标志”，从而使别的线程有机会抢占该锁。
  当前线程必须拥有当前对象锁。如果当前线程不是此锁的拥有者，会抛出IllegalMonitorStateException异常。
  唤醒当前对象锁的等待线程使用notify或notifyAll方法，也必须拥有相同的对象锁，否则也会抛出IllegalMonitorStateException异常。
  waite()和notify()必须在synchronized函数或synchronized　block中进行调用。如果在non-synchronized函数或non-synchronized　block中进行调用，虽然能编译通过，但在运行时会发生IllegalMonitorStateException的异常
  ```

- 说说 CountDownLatch 原理,说说 CyclicBarrier 原理,说说 Semaphore 原理

  ```
  1）CountDownLatch和CyclicBarrier都能够实现线程之间的等待，只不过它们侧重点不同：
  
  CountDownLatch一般用于某个线程A等待若干个其他线程执行完任务之后，它才执行；
  
  而CyclicBarrier一般用于一组线程互相等待至某个状态，然后这一组线程再同时执行；
  
  另外，CountDownLatch是不能够重用的，而CyclicBarrier是可以重用的。
  
  2）Semaphore其实和锁有点类似，它一般用于控制对某组资源的访问权限。
  ```

- 说说 Exchanger 原理

  ```
  Exchanger（交换者）是一个用于线程间协作的工具类。Exchanger用于进行线程间的数据交换。它提供一个同步点，在这个同步点两个线程可以交换彼此的数据。这两个线程通过exchange方法交换数据， 如果第一个线程先执行exchange方法，它会一直等待第二个线程也执行exchange，当两个线程都到达同步点时，这两个线程就可以交换数据，将本线程生产出来的数据传递给对方。因此使用Exchanger的重点是成对的线程使用exchange()方法，当有一对线程达到了同步点，就会进行交换数据。因此该工具类的线程对象是成对的。
  
         Exchanger类提供了两个方法，String exchange(V x):用于交换，启动交换并等待另一个线程调用exchange；String exchange(V x,long timeout,TimeUnit unit)：用于交换，启动交换并等待另一个线程调用exchange，并且设置最大等待时间，当等待时间超过timeout便停止等待。
  ```

- 说说 CountDownLatch 与 CyclicBarrier 区别

- ThreadLocal 原理分析

  ```
  # 简述
  当我们只想在本身的线程内使用的变量，可以用 ThreadLocal 来实现，并且这些变量是和线程的生命周期密切相关的，线程结束，变量也就销毁了。
  它是线程的局部变量，这些变量只能在这个线程内被读写，在其他线程内是无法访问的。 ThreadLocal 定义的通常是与线程关联的私有静态字段（例如，用户ID或事务ID）。
  
  # 使用场景
  1、比如线程中处理一个非常复杂的业务，可能方法有很多，那么，使用 ThreadLocal 可以代替一些参数的显式传递；
  2、比如用来存储用户 Session。Session 的特性很适合 ThreadLocal ，因为 Session 之前当前会话周期内有效，会话结束便销毁。我们先笼统但不正确的分析一次 web 请求的过程：
  用户在浏览器中访问 web 页面；
  浏览器向服务器发起请求；
  服务器上的服务处理程序（例如tomcat）接收请求，并开启一个线程处理请求，期间会使用到 Session ；
  最后服务器将请求结果返回给客户端浏览器。
  从这个简单的访问过程我们看到正好这个 Session 是在处理一个用户会话过程中产生并使用的，如果单纯的理解一个用户的一次会话对应服务端一个独立的处理线程，那用 ThreadLocal 在存储 Session ,简直是再合适不过了。但是例如 tomcat 这类的服务器软件都是采用了线程池技术的，并不是严格意义上的一个会话对应一个线程。并不是说这种情况就不适合 ThreadLocal 了，而是要在每次请求进来时先清理掉之前的 Session ，一般可以用拦截器、过滤器来实现。
  3、在一些多线程的情况下，如果用线程同步的方式，当并发比较高的时候会影响性能，可以改为 ThreadLocal 的方式，例如高性能序列化框架 Kyro 就要用 ThreadLocal 来保证高性能和线程安全；
  4、还有像线程内上线文管理器、数据库连接等可以用到 ThreadLocal;
  
  # 如何使用
  ThreadLocal 的使用非常简单，最核心的操作就是四个：创建、创建并赋初始值、赋值、取值
  
  首先 ThreadLocal 是一个泛型类，保证可以接受任何类型的对象。
  因为一个线程内可以存在多个 ThreadLocal 对象，所以其实是 ThreadLocal 内部维护了一个 Map ，这个 Map 不是直接使用的 HashMap ，而是 ThreadLocal 实现的一个叫做 ThreadLocalMap 的静态内部类。而我们使用的 get()、set() 方法其实都是调用了这个 ThreadLocalMap 类对应的 get()、set() 方法。例如下面的 set 方法：
  
  public void set(T value) {
          Thread t = Thread.currentThread();
          ThreadLocalMap map = getMap(t);
          if (map != null)
              map.set(this, value);
          else
              createMap(t, value);
      }
  调用 ThreadLocal 的 set 方法时，首先获取到了当前线程，然后获取当前线程维护的 ThreadLocalMap 对象，最后在ThreadLocalMap 实例中添加上。如果 ThreadLocalMap 实例不存在则初始化并赋初始值。
  
  这里看到 set 方法的第一个参数是 this ，this即指的是当前的 ThreadLocal 对象，会看上看的代码就是指的 mLocal 这个对象。而在 ThreadLocalMap 的 set 方法中会根据当前 ThreadLocal 对象实例，做一些操作和判断，最终实现赋值操作（具体参考源码）。
  
  所以说，最终的变量是放在了当前线程的 ThreadLocalMap 中，并不是存在 ThreadLocal 上，ThreadLocal 可以理解为只是一个中间工具，传递了变量值。
  
  # 注意事项
  使用 ThreadLocal 的时候，最好不要声明为静态的；
  使用完 ThreadLocal ，最好手动调用 remove() 方法，例如上面说到的 Session 的例子，如果不在拦截器或过滤器中处理，不仅可能出现内存泄漏问题，而且会影响业务逻辑
  ```

- 讲讲线程池的实现原理

  ```
  # 好处
  1、降低资源消耗；
  2、提高响应速度；
  3、提高线程的可管理性
  
  # ThreadPoolExecutor
  Executors是java线程池的工厂类，通过它可以快速初始化一个符合业务需求的线程池，如Executors.newFixedThreadPool方法可以生成一个拥有固定线程数的线程池。
  其本质是通过不同的参数初始化一个ThreadPoolExecutor对象，具体参数描述如下：
  # corePoolSize
  线程池中的核心线程数，当提交一个任务时，线程池创建一个新线程执行任务，直到当前线程数等于corePoolSize；如果当前线程数为corePoolSize，继续提交的任务被保存到阻塞队列中，等待被执行；如果执行了线程池的prestartAllCoreThreads()方法，线程池会提前创建并启动所有核心线程。
  # maximumPoolSize
  线程池中允许的最大线程数。如果当前阻塞队列满了，且继续提交任务，则创建新的线程执行任务，前提是当前线程数小于maximumPoolSize；
  # keepAliveTime
  线程空闲时的存活时间，即当线程没有任务执行时，继续存活的时间；默认情况下，该参数只在线程数大于corePoolSize时才有用；
  # unit
  keepAliveTime的单位；
  # workQueue
  用来保存等待被执行的任务的阻塞队列，且任务必须实现Runable接口，在JDK中提供了如下阻塞队列：
  1、ArrayBlockingQueue：基于数组结构的有界阻塞队列，按FIFO排序任务；
  2、LinkedBlockingQuene：基于链表结构的阻塞队列，按FIFO排序任务，吞吐量通常要高于ArrayBlockingQuene；
  3、SynchronousQuene：一个不存储元素的阻塞队列，每个插入操作必须等到另一个线程调用移除操作，否则插入操作一直处于阻塞状态，吞吐量通常要高于LinkedBlockingQuene；
  4、priorityBlockingQuene：具有优先级的无界阻塞队列；
  # threadFactory
  创建线程的工厂，通过自定义的线程工厂可以给每个新建的线程设置一个具有识别度的线程名。
  # handler
  线程池的饱和策略，当阻塞队列满了，且没有空闲的工作线程，如果继续提交任务，必须采取一种策略处理该任务，线程池提供了4种策略：
  1、AbortPolicy：直接抛出异常，默认策略；
  2、CallerRunsPolicy：用调用者所在的线程来执行任务；
  3、DiscardOldestPolicy：丢弃阻塞队列中靠最前的任务，并执行当前任务；
  4、DiscardPolicy：直接丢弃任务；
  当然也可以根据应用场景实现RejectedExecutionHandler接口，自定义饱和策略，如记录日志或持久化存储不能处理的任务。
  # Exectors
  Exectors工厂类提供了线程池的初始化接口，主要有如下几种：
  1. newFixedThreadPool
  初始化一个指定线程数的线程池，其中corePoolSize == maximumPoolSize，使用LinkedBlockingQuene作为阻塞队列，不过当线程池没有可执行任务时，也不会释放线程。
  2. newCachedThreadPool
  1、初始化一个可以缓存线程的线程池，默认缓存60s，线程池的线程数可达到Integer.MAX_VALUE，即2147483647，内部使用SynchronousQueue作为阻塞队列；
  2、和newFixedThreadPool创建的线程池不同，newCachedThreadPool在没有任务执行时，当线程的空闲时间超过keepAliveTime，会自动释放线程资源，当提交新任务时，如果没有空闲线程，则创建新线程执行任务，会导致一定的系统开销；
  所以，使用该线程池时，一定要注意控制并发的任务数，否则创建大量的线程可能导致严重的性能问题。
  3. newSingleThreadExecutor
  初始化的线程池中只有一个线程，如果该线程异常结束，会重新创建一个新的线程继续执行任务，唯一的线程可以保证所提交任务的顺序执行，内部使用LinkedBlockingQueue作为阻塞队列。
  4. newScheduledThreadPool
  初始化的线程池可以在指定的时间内周期性的执行所提交的任务，在实际的业务场景中可以使用该线程池定期的同步数据。
  ```

- 线程池的几种方式与使用场景

- 线程的生命周期

### 锁机制

- 说说线程安全问题

  ```
  保证类线程安全的措施：
  1. 不共享线程间的变量；
  2. 设置属性变量为不可变变量；
  3. 每个共享的可变变量都使用一个确定的锁保护；
  
  保证线程安全的思路：
  1. 通过架构设计
  通过上层的架构设计和业务分析来避免并发场景。比如需要用多线程或分布式集群统计一堆用户的相关统计值，由于用户的统计值是共享数据，因此需要保证线程安全。从业务上分析出用户之间的数据并不共享，因此可以设计一个规则来保证一个用户的计算工作和数据访问只被一个线程或一台机器完成，这样从设计上避免了接下来可能的并发问题。
  
  2. 保证类无状态
  有状态会限制横向扩展能力，也可能产生并发问题。如果类是无状态的，那它永远是线程安全的。因此在设计阶段尽可能用无状态的类来满足业务需求。
  
  3. 区别原子操作和复合操作
  常见的复合操作包括check-then-act, i++等。虽然check-then-act从表面上看很简单，但却普遍存在与我们日常的开发中，特别是在数据库存取这一块。比如我们需要在数据库里存一个客户的统计值，当统计值不存在时初始化，当存在时就去更新。如果不把这组逻辑设计为原子性的就很有可能产生出两条这个客户的统计值。
  在单机环境下处理这个问题还算容易，通过锁或者同步来把这组复合操作变为原子操作，但在分布式环境下就不适用了。一般情况下是通过在数据库端做文章，比如通过唯一性索引或者悲观锁来保障其数据一致性。当然任何方案都是有代价的，这就需要具体情况下来权衡。
  
  4. 锁
  使用锁应注意：
  
  每个共享变量必须由一个确定的锁保护。
  使用锁会有性能损失
  锁不能解决在分布式环境共享变量的并发问题
  ```

  

- volatile 实现原理

  ```
  当一个变量定义为volatile之后，它具备两种特性：
  
  保证此变量对所有线程的可见性，这里的“可见性”是指当一条线程修改了这个变量的值，新值对于其他线程来说是可以立即得知的。
  
  禁止指令重排序优化。
  
  在X86处理器下通过工具获取 JIT编译器生成的汇编指令来看下volatile变量进行读写操作时CPU的行为：
  Java 代码如下：
  
  // volatile Object instance;
  instance = new Singleton();
  生成的汇编代码如下：
  
  0x01a3de1d: movb $0X0, 0X1104800(%esi); 0X01a3de24: lock addl $0X0, (%esp);
  有volatile变量修饰的共享变量进行写操作的时候会多出第二行汇编代码，Lock前缀的指令在多核处理器下会引发了两件事件。
  
  将当前处理器缓存的数据写回到系统内存。
  
  这个写回内存的操作会使在其他CPU里缓存了该内存地址的数据无效。
  
  再让我们从Java内存模型的角度分析下volatile变量。假定T表示一个线程，V和W分别表示两个volatile变量，那么在进行read, load, use, assign, store和write时需要满足以下三条规则：
  
  只有当线程T对变量V执行的前一个动作是load时，T才能对V执行use; 并且，只有当T对V执行的后一个动作是use时，T才能对V执行load。T对V的use动作可以认为是和线程T对V的load，read动作相关联，必须连续一起出现（这条规则要求 在工作内存中，每次使用V前都必须先从主内存刷新最新的值，用于保证能看见其他线程对变量V所做的修改后的值）。
  
  只有当线程T对变量V执行的前一个动作是assign时，T才能对V执行store动作；并且，只有当T对变量V执行的后一个动作是store时，线程T才能对变量V执行assign动作。线程T对变量V的assign动作可认为是和线程T对变量V的store, write动作相关联，必须连续一起出现（这条规则要求 在工作内存中，每次修改V后都必须立刻同步回主内存中，用于保证其他线程可以看到自己对变量V所做的修改）。
  
  假定动作A是线程T对变量V实施的use或assign操作，假定动作F是和动作A相关联的load或store动作，假定动作P是和动作F相应的变量V的read或write动作；类似的，假定动作B是线程T对变量W实施的use或assign动作，假定动作G是和动作B相关联的load或store动作，假定动作Q是和动作G相应的变量W的read或write动作。如果A先于B，那P先于Q（这条规则要求 volatile修饰的变量不会被指令重排序优化，保证代码的执行顺序与程序的顺序相同）。
  
  由于volatile变量只能保证可见性，在不符合以下两条规则的运算场景中，仍然要通过加锁（使用synchronized或java.util.concurrent中的原子类）来保证原子性：
  
  运行结果并不依赖变量的当前值，或者能够确保只有单一的线程修改变量的值。
  
  变量不需要与其他的状态变量共同参与不变约束。
  
  在某些情况下，volatile的同步机制性要优于锁。并且，volatile变量读操作的性能消耗与普通变量几乎没有什么差别，但是写操作则可能会慢一些，因为它需要在本地代码中插入许多内存屏障指令来保证处理器不发生乱序执行。
  ```

  

- synchronize 实现原理

  ```
  　Synchronized是Java中解决并发问题的一种最常用的方法，也是最简单的一种方法。Synchronized的作用主要有三个：（1）确保线程互斥的访问同步代码（2）保证共享变量的修改能够及时可见（3）有效解决重排序问题。从语法上讲，Synchronized总共有三种用法：
  　　（1）修饰普通方法
  　　（2）修饰静态方法
  　　（3）修饰代码块
  　　
  	Synchronized的实现原理，Synchronized的语义底层是通过一个monitor的对象来完成，其实wait/notify等方法也依赖于monitor对象，这就是为什么只有在同步的块或者方法中才能调用wait/notify等方法，否则会抛出java.lang.IllegalMonitorStateException的异常的原因。
  　
  　每个对象有一个监视器锁（monitor）。当monitor被占用时就会处于锁定状态，线程执行monitorenter指令时尝试获取monitor的所有权，过程如下：
  1、如果monitor的进入数为0，则该线程进入monitor，然后将进入数设置为1，该线程即为monitor的所有者。
  2、如果线程已经占有该monitor，只是重新进入，则进入monitor的进入数加1.
  3.如果其他线程已经占用了monitor，则该线程进入阻塞状态，直到monitor的进入数为0，再重新尝试获取monitor的所有权
  	执行monitorexit的线程必须是objectref所对应的monitor的所有者。
  指令执行时，monitor的进入数减1，如果减1后进入数为0，那线程退出monitor，不再是这个monitor的所有者。其他被这个monitor阻塞的线程可以尝试去获取这个 monitor 的所有权。 
  
  JDK1.6以后，为了减少获得锁和释放锁所带来的性能消耗，提高性能，引入了“轻量级锁”和“偏向锁”。
  锁的状态总共有四种：无锁状态、偏向锁、轻量级锁和重量级锁
  ```


| **锁状态** | 25 bit                       | 4bit         | 1bit         | 2bit |      |
| ---------- | ---------------------------- | ------------ | ------------ | ---- | ---- |
| 23bit      | 2bit                         | 是否是偏向锁 | 锁标志位     |      |      |
| 轻量级锁   | 指向栈中锁记录的指针         | 00           |              |      |      |
| 重量级锁   | 指向互斥量（重量级锁）的指针 | 10           |              |      |      |
| GC标记     | 空                           | 11           |              |      |      |
| 偏向锁     | 线程ID                       | Epoch        | 对象分代年龄 | 1    | 01   |
| 无锁       | 对象的hashCode               | 对象分代年龄 | 0            | 01   |      |

  synchronized 与 lock 的区别

- ```
  1、ReentrantLock 拥有Synchronized相同的并发性和内存语义，此外还多了 锁投票，定时锁等候和中断锁等候
  线程A和B都要获取对象O的锁定，假设A获取了对象O锁，B将等待A释放对O的锁定，
  如果使用 synchronized ，如果A不释放，B将一直等下去，不能被中断
  如果 使用ReentrantLock，如果A不释放，可以使B在等待了足够长的时间以后，中断等待，而干别的事情
  
  ReentrantLock获取锁定与三种方式：
  a) lock(), 如果获取了锁立即返回，如果别的线程持有锁，当前线程则一直处于休眠状态，直到获取锁
  b) tryLock(), 如果获取了锁立即返回true，如果别的线程正持有锁，立即返回false；
  c)tryLock(long timeout,TimeUnit unit)， 如果获取了锁定立即返回true，如果别的线程正持有锁，会等待参数给定的时间，在等待的过程中，如果获取了锁定，就返回true，如果等待超时，返回false；
  d) lockInterruptibly:如果获取了锁定立即返回，如果没有获取锁定，当前线程处于休眠状态，直到或者锁定，或者当前线程被别的线程中断
  
  2、synchronized是在JVM层面上实现的，不但可以通过一些监控工具监控synchronized的锁定，而且在代码执行时出现异常，JVM会自动释放锁定，但是使用Lock则不行，lock是通过代码实现的，要保证锁定一定会被释放，就必须将unLock()放到finally{}中
  
  3、在资源竞争不是很激烈的情况下，Synchronized的性能要优于ReetrantLock，但是在资源竞争很激烈的情况下，Synchronized的性能会下降几十倍，但是ReetrantLock的性能能维持常态；
  
  synchronized： 
  在资源竞争不是很激烈的情况下，偶尔会有同步的情形下，synchronized是很合适的。原因在于，编译程序通常会尽可能的进行优化synchronize，另外可读性非常好，不管用没用过5.0多线程包的程序员都能理解。
  
  ReentrantLock: 
  ReentrantLock提供了多样化的同步，比如有时间限制的同步，可以被Interrupt的同步（synchronized的同步是不能Interrupt的）等。在资源竞争不激烈的情形下，性能稍微比synchronized差点点。但是当同步非常激烈的时候，synchronized的性能一下子能下降好几十倍。而ReentrantLock确还能维持常态。
  
  Atomic: 
  和上面的类似，不激烈情况下，性能比synchronized略逊，而激烈的时候，也能维持常态。激烈的时候，Atomic的性能会优于ReentrantLock一倍左右。但是其有一个缺点，就是只能同步一个值，一段代码中只能出现一个Atomic的变量，多于一个同步无效。因为他不能在多个Atomic之间同步。
  
  
  所以，我们写同步的时候，优先考虑synchronized，如果有特殊需要，再进一步优化。ReentrantLock和Atomic如果用的不好，不仅不能提高性能，还可能带来灾难。
  ```

- CAS 乐观锁

  ```
  synchronized是悲观锁，这种线程一旦得到锁，其他需要锁的线程就挂起的情况就是悲观锁。
  CAS操作的就是乐观锁，每次不加锁而是假设没有冲突而去完成某项操作，如果因为冲突失败就重试，直到成功为止
  
  CAS是英文单词Compare And Swap的缩写，翻译过来就是比较并替换。
  CAS机制当中使用了3个基本操作数：内存地址V，旧的预期值A，要修改的新值B。
  更新一个变量的时候，只有当变量的预期值A和内存地址V当中的实际值相同时，才会将内存地址V对应的值修改为B。
  
  CAS的缺点：
  1.CPU开销较大
  在并发量比较高的情况下，如果许多线程反复尝试更新某一个变量，却又一直更新不成功，循环往复，会给CPU带来很大的压力。
  2.不能保证代码块的原子性
  CAS机制所保证的只是一个变量的原子性操作，而不能保证整个代码块的原子性。比如需要保证3个变量共同进行原子性的更新，就不得不使用Synchronized了。
  
  ```

  

- ABA 问题

  ```
  1、可以发现，CAS实现的过程是先取出内存中某时刻的数据，在下一时刻比较并替换，那么在这个时间差会导致数据的变化，此时就会导致出现“ABA”问题。 
  2、什么是”ABA”问题？ 
  比如说一个线程one从内存位置V中取出A，这时候另一个线程two也从内存中取出A，并且two进行了一些操作变成了B，然后two又将V位置的数据变成A，这时候线程one进行CAS操作发现内存中仍然是A，然后one操作成功。 
  尽管线程one的CAS操作成功，但是不代表这个过程就是没有问题的。
  
  使用 AtomicStampedReference，AtomicMarkableReference解决ABA问题
  AtomicStampedReference 本质是有一个int 值作为版本号，每次更改前先取到这个int值的版本号，等到修改的时候，比较当前版本号与当前线程持有的版本号是否一致，如果一致，则进行修改，并将版本号+1（当然加多少或减多少都是可以自己定义的），在zookeeper中保持数据的一致性也是用的这种方式；
  AtomicMarkableReference则是将一个boolean值作是否有更改的标记，本质就是它的版本号只有两个，true和false，修改的时候在这两个版本号之间来回切换，这样做并不能解决ABA的问题，只是会降低ABA问题发生的几率而已；
  
  ```

- 乐观锁的业务场景及实现方式

- AQS

  ```
  AQS，即AbstractQueuedSynchronizer, 队列同步器，它是Java并发用来构建锁和其他同步组件的基础框架。
  AQS是一个抽象类，主是是以继承的方式使用。AQS本身是没有实现任何同步接口的，它仅仅只是定义了同步状态的获取和释放的方法来供自定义的同步组件的使用。从图中可以看出，在java的同步组件中，AQS的子类（Sync等）一般是同步组件的静态内部类，即通过组合的方式使用。
  AQS的实现依赖内部的同步队列（FIFO双向队列），如果当前线程获取同步状态失败，AQS会将该线程以及等待状态等信息构造成一个Node，将其加入同步队列的尾部，同时阻塞当前线程，当同步状态释放时，唤醒队列的头节点。
  上面说的有点抽象，来具体看下，首先来看AQS最主要的三个成员变量：
  
      private transient volatile Node head;
      
      private transient volatile Node tail;
  
      private volatile int state;
      
  上面提到的同步状态就是这个int型的变量state. head和tail分别是同步队列的头结点和尾结点。假设state=0表示同步状态可用（如果用于锁，则表示锁可用），state=1表示同步状态已被占用（锁被占用）。
  
  下面举例说下获取和释放同步状态的过程：
  
  获取同步状态
  
  假设线程A要获取同步状态（这里想象成锁，方便理解），初始状态下state=0,所以线程A可以顺利获取锁，A获取锁后将state置为1。在A没有释放锁期间，线程B也来获取锁，此时因为state=1，表示锁被占用，所以将B的线程信息和等待状态等信息构成出一个Node节点对象，放入同步队列，head和tail分别指向队列的头部和尾部（此时队列中有一个空的Node节点作为头点，head指向这个空节点，空Node的后继节点是B对应的Node节点，tail指向它），同时阻塞线程B(这里的阻塞使用的是LockSupport.park()方法)。后续如果再有线程要获取锁，都会加入队列尾部并阻塞。
  
  释放同步状态
  当线程A释放锁时，即将state置为0，此时A会唤醒头节点的后继节点（所谓唤醒，其实是调用LockSupport.unpark(B)方法），即B线程从LockSupport.park()方法返回，此时B发现state已经为0，所以B线程可以顺利获取锁，B获取锁后B的Node节点随之出队。
  
  上面只是简单介绍了AQS获取和释放的大致过程，下面结合AQS和ReentrantLock源码来具体看下JDK是如何实现的，特别要注意JDK是如何保证同步和并发操作的。
  ```

- JUC

  ```
  J.U.C并发包，即java.util.concurrent包，是JDK的核心工具包，是JDK1.5之后，由 Doug Lea实现并引入。
  
  整个java.util.concurrent包，按照功能可以大致划分如下：
  
  juc-locks 锁框架
  juc-atomic 原子类框架
  juc-sync 同步器框架
  juc-collections 集合框架
  juc-executors 执行器框架
  ```

- 互斥锁、读写锁和自旋锁

- ```
  # 读写锁有三种状态：读加锁状态、写加锁状态和不加锁状态 
  只有一个线程可以占有写状态的锁，但可以有多个线程同时占有读状态锁，这也是它可以实现高并发的原因。当其处于写状态锁下，任何想要尝试获得锁的线程都会被阻塞，直到写状态锁被释放；如果是处于读状态锁下，允许其它线程获得它的读状态锁，但是不允许获得它的写状态锁，直到所有线程的读状态锁被释放；为了避免想要尝试写操作的线程一直得不到写状态锁，当处于读模式的读写锁接收到一个试图对其进行写模式加锁操作时，便会阻塞后面对其进行读模式加锁操作的线程。 即当读写锁感知到有线程想要获得写状态锁时，便会阻塞其后所有想要获得读状态锁的线程。这样当读模式的锁解锁后，要获得写状态锁的线程能够访问此锁保护的资源。所以读写锁非常适合资源的读操作远多于写操作的情况。
  
  # 互斥锁
  在访问共享资源之前对进行加锁操作，在访问完成之后进行解锁操作。 加锁后，任何其他试图再次加锁的线程会被阻塞，直到当前线程解锁。 如果解锁时有一个以上的线程阻塞，那么所有该锁上的线程都被编程就绪状态， 第一个变为就绪状态的线程又执行加锁操作，那么其他的线程又会进入等待。 在这种方式下，只有一个线程能够访问被互斥锁保护的资源。
  
  # 自旋锁
  自旋锁是一种特殊的互斥锁，当资源被枷锁后，其他线程想要再次加锁，此时该线程不会被阻塞睡眠而是陷入循环等待状态（CPU不能做其它事情），循环检查资源持有者是否已经释放了资源，这样做的好处是减少了线程从睡眠到唤醒的资源消耗，但会一直占用CPU的资源。适用于资源的锁被持有的时间短，而又不希望在线程的唤醒上花费太多资源的情况
  
  从 实现原理上来讲，互斥锁属于sleep-waiting(睡眠等待)类型的锁。例如在一个双核的机器上有两个线程(线程A和线程B)，它们分别运行在Core0和 Core1上。假设线程A想要通过pthread_mutex_lock操作去得到一个临界区的锁，而此时这个锁正被线程B所持有，那么线程A就会被阻塞 (blocking)，Core0 会在此时进行上下文切换(Context Switch)将线程A置于等待队列中，此时Core0就可以运行其他的任务(例如另一个线程C)而不必进行忙等待。而自旋锁则不然，它属于busy-waiting(忙等待)类型的锁，如果线程A是使用pthread_spin_lock操作去请求锁，那么线程A就会一直在 Core0上进行忙等待并不停的进行锁请求，直到得到这个锁为止
  ```

- JVM调优

    ```
    JVM的调优主要是内存的调优，主要调两个方面：各个代的大小,垃圾收集器选择;
    原则
    
    在实际开发中，前台不要使用jsp，使用velocity等模板引擎技术
    
    不要引入无关的jar
    
    -XX:SurvivorRatio过大：对象在年轻代的存活时间变长，可能在年轻代就被回收掉而不必进入年老代，但是相应的复制的时候survivor区就会被占用更多的空间。
    
    -XX:SurvivorRatio过大：对象在年轻代的存活时间变短，可能会早早进入年老代而失去在年轻代被回收的机会，但是相应的复制的时候survivor区也就有更多内存了，这样可能会避免部分大对象直接进入年老代
    
    -XX:SurvivorRatio过大：Eden变大，Survivor变小，minor GC可能减少，但是由于suvivor减小了，所以如果minor GC存活下来的对象大于suvivor，则会直接进入年老代
    
    -XX:SurvivorRatio过小：Eden变小，Survivor变大，minor GC可能增多，但是由于suvivor变大了，能够存储更多存活下来的对象，进入年老代的对象可能会减少
    
    
    调节时机：minor GC太频繁
    
    -Xmn过小：minor GC太频繁；小对象可能也会直接进入年老代，提前导致Full GC
    
    -Xmn过大：年轻代大了，minor GC的时间变长了；年老代变小了，Full GC会频繁
    
    调节策略：若-Xmx可调大，则调大，且保持-Xmn==-Xmx/4~-Xmx/3；若-Xmx不可调大，在保持-Xmn==-Xmx/4~-Xmx/3的范围内增大-Xmn，若-Xmn也不可调了，则试着调大-XX:SurvivorRatio来看看情况
    
    -Xmx==-Xms：防止堆内存频繁进行调整，调整的时机见《第一章 JVM内存结构》
    
    -Xmn：通常设为-Xmx/4（这是我在企业中实习时的设置方式，系统运行正常、平稳、速度也快），林昊推荐的是-Xmx/3，所以-Xmn==-Xmx/4~-Xmx/3
    
    -XX:SurvivorRatio：默认8
    
    -XX:MaxTenuringThreshold：默认为15
    
    -XX:MaxPermSize==-XX:PermSize
    
    垃圾收集器选择
    
    企业中最常用的两个组合：
    
    Parallel Scavenge/Parallel Old
    
    注重吞吐量（吞吐量越大，说明CPU利用率越高）
    
    主要用于处理很多的CPU计算任务而用户交互任务较少的情况
    
    也用于让JVM自动调优而我们袖手旁观的情况（-XX:+UseParallelOldGC，-XX:GCTimeRatio，-Xmx，-XX:+UseAdaptiveSizePolicy）
    
    -XX:+UseParallelOldGC：指定使用该组合
    
    ParNew/CMS
    
    注重STW的缩短（该时间越短，用户体验越好，而且会减少部分请求的请求超时问题）
    
    -XX:+UseConcMarkSweepGC：指定使用该组合
    
    -XX:CMSInitiatingOccupancyFraction：来指定当年老代空间满了多少后（百分比）进行垃圾回收
    
    关于上边两种组合的说明
    
    一般而言，在企业中，机器的CPU数量都比较多，且CPU的计算能力也不会成为瓶颈，所以对于CMS的并发标记与并发清除阶段，会占用CPU资源的问题，其实不是大事儿；而对于Parallel的注重吞吐量的问题也就不是什么大事儿了，毕竟CPU是强大的
    
    所以，ParNew/CMS是首选（在G1不能用的情况下），Parallel Scavenge/Parallel Old只在想让JVM自动管理内存的情况下使用
    ```

    

## 核心篇

### 数据存储

- Mysql单表

  ```
  阿里巴巴《Java 开发手册》提出单表行数超过 500 万行或者单表容量超过 2GB，才推荐进行分库分表。对此，有阿里的黄金铁律支撑，所以，很多人设计大数据存储时，多会以此为标准，进行分表操作。
  InnoDB buffer size 足够的情况下，其能完成全加载进内存，查询不会有问题。但是，当单表数据库到达某个量级的上限时，导致内存无法存储其索引，使得之后的 SQL 查询会产生磁盘 IO，从而导致性能下降
  ```

- [MySQL 索引使用的注意事项]

  ```
  1. 不要在列上使用函数和进行运算
  2. 尽量避免使用 != 或 not in或 <> 等否定操作符
  3. 尽量避免使用 or 来连接条件
  4. 多个单列索引并不是最佳选择
  5. 复合索引的最左前缀原则
  6. 覆盖索引的好处
  7. 范围查询对多列查询的影响
  8. 索引不会包含有NULL值的列
  9. 隐式转换的影响
  10. like 语句的索引失效问题
  ```

  

- Mysql索引

  ```
  1. 基本索引类型
  1.1. 单列索引
  1.2. 复合索引
  1.3. 唯一索引
  1.4. 主键索引
  2. 强制索引:有时，因为使用 MySQL 的优化器机制，原本应该使用索引的优化器，反而选择执行全表扫描或者执行的不是预期的索引。此时，可以通过强制索引的方式引导优化器采取正确的执行计划。
  使用强制索引，SQL 语句只使用建立在 index_col_name 上的索引，而不使用其它的索引
  3. 全文索引:在一般情况下，模糊查询都是通过 like 的方式进行查询。但是，对于海量数据，这并不是一个好办法，在 like “value%” 可以使用索引，但是对于 like “%value%” 这样的方式，执行全表查询，这在数据量小的表，不存在性能问题，但是对于海量数据，全表扫描是非常可怕的事情,所以 like 进行模糊匹配性能很差。
  这种情况下，需要考虑使用全文搜索的方式进行优化。全文搜索在 MySQL 中是一个 FULLTEXT 类型索引。 FULLTEXT 索引在 MySQL 5.6 版本之后支持 InnoDB，而之前的版本只支持 MyISAM 表。
  临时方案
  为中文内容表提供一个全文索引表，存储全文索引分词信息，两张表根据中文内容表的 ID 进行关联。
  将内容进行分词后，用 base64 编码，保存在全文索引表中。
  关键的一步，如何分词，分词的命中率问题。很简单，自定义分词库，写一个分词算法将所有的组合进行分词，在内容不多的情况下非常有用。举个例子，“梁桂钊”，可以进行自定义分词：[梁、桂、钊、梁桂、桂钊、梁桂钊]。
  ```

- [说说反模式设计]

- [说说分库与分表设计]

- [分库与分表带来的分布式困境与应对之策]

  ```
  数据迁移与扩容问题
  前面介绍到水平分表策略归纳总结为随机分表和连续分表两种情况。连续分表有可能存在数据热点的问题，有些表可能会被频繁地查询从而造成较大压力，热数据的表就成为了整个库的瓶颈，而有些表可能存的是历史数据，很少需要被查询到。连续分表的另外一个好处在于比较容易，不需要考虑迁移旧的数据，只需要添加分表就可以自动扩容。随机分表的数据相对比较均匀，不容易出现热点和并发访问的瓶颈。但是，分表扩展需要迁移旧的数据。
  针对于水平分表的设计至关重要，需要评估中短期内业务的增长速度，对当前的数据量进行容量规划，综合成本因素，推算出大概需要多少分片。对于数据迁移的问题，一般做法是通过程序先读出数据，然后按照指定的分表策略再将数据写入到各个分表中。
  
  表关联问题
  在单库单表的情况下，联合查询是非常容易的。但是，随着分库与分表的演变，联合查询就遇到跨库关联和跨表关系问题。在设计之初就应该尽量避免联合查询，可以通过程序中进行拼装，或者通过反范式化设计进行规避。
  
  分页与排序问题
  一般情况下，列表分页时需要按照指定字段进行排序。在单库单表的情况下，分页和排序也是非常容易的。但是，随着分库与分表的演变，也会遇到跨库排序和跨表排序问题。为了最终结果的准确性，需要在不同的分表中将数据进行排序并返回，并将不同分表返回的结果集进行汇总和再次排序，最后再返回给用户。
  
  分布式事务问题
  随着分库与分表的演变，一定会遇到分布式事务问题，那么如何保证数据的一致性就成为一个必须面对的问题。目前，分布式事务并没有很好的解决方案，难以满足数据强一致性，一般情况下，使存储数据尽可能达到用户一致，保证系统经过一段较短的时间的自我恢复和修正，数据最终达到一致。
  
  分布式全局唯一ID
  在单库单表的情况下，直接使用数据库自增特性来生成主键ID，这样确实比较简单。在分库分表的环境中，数据分布在不同的分表上，不能再借助数据库自增长特性。需要使用全局唯一 ID，例如 UUID、GUID等。关于如何选择合适的全局唯一 ID，我会在后面的章节中进行介绍。
  
  总结
  分库与分表主要用于应对当前互联网常见的两个场景：海量数据和高并发。然而，分库与分表是一把双刃剑，虽然很好的应对海量数据和高并发对数据库的冲击和压力，但是却提高的系统的复杂度和维护成本。
  
  因此，我的建议：需要结合实际需求，不宜过度设计，在项目一开始不采用分库与分表设计，而是随着业务的增长，在无法继续优化的情况下，再考虑分库与分表提高系统的性能。
  
  工具： TDDl，myCat
  ```

- [说说 SQL 优化之道]

- MySQL 遇到的死锁问题

- [存储引擎的 InnoDB 与 MyISAM]

  ```
  作为 MySQL 数据库的两种主要的存储引擎，InnoDB 与 MyISAM 各有长处。
  
  在 MySQL 5.1 及之前的版本中，MyISAM 是默认的存储引擎，而在 MySQL 5.5 版本以后，默认使用 InnoDB 存储引擎。
  
  MyISAM 不支持行级锁，换句话说，MyISAM 会对整张表加锁，而不是针对行。同时，MyISAM 不支持事务和外键。MyISAM 可被压缩，存储空间较小，而且 MyISAM 在筛选大量数据时非常快。
  
  InnoDB 是事务型引擎，当事务异常提交时，会被回滚。同时，InnoDB 支持行锁。此外，InnoDB 需要更多存储空间，会在内存中建立其专用的缓冲池用于高速缓冲数据和索引。InnoDB 支持自动奔溃恢复特性。
  
  InnoDB 与 MyISAM 的主要区别
  
  方面	MyISAM	InnoDB
  事务	不支持	支持
  外键	不支持	支持
  行级锁	不支持	支持
  自动奔溃恢复	不支持	支持
  对于如何选择 InnoDB 与 MyISAM 存储引擎，我的建议：一般情况下，应该优先选择 InnoDB 存储引擎，并且尽量不要将 InnoDB 与 MyISAM 混合使用。
  ```

  

- 数据库索引的原理

- 为什么要用 B-tree

- 聚集索引与非聚集索引的区别

- limit 20000 加载很慢怎么解决

- 选择合适的分布式主键方案

- [选择合适的数据存储方案](https://link.jianshu.com?t=http%3A%2F%2Fblog.720ui.com%2F2017%2Fdb_better_db_use%2F)

- ObjectId 规则

- [聊聊 MongoDB 使用场景](https://link.jianshu.com?t=http%3A%2F%2Fblog.720ui.com%2F2017%2Fmongodb_core_use%2F)

- 倒排索引

- 聊聊 ElasticSearch 使用场景

- MongoDB

  ```
  在介绍 MongoDB 能做什么之前，先来了解下 MongoDB 不能做什么事情。MongoDB是对传统关系型数据库的补充，但是 MongoDB 不支持事务，因此对事务性有要求的程序不建议使用 MongoDB。此外，MongoDB 也不支持表联合查询，而这个是关系型数据库擅长的事情。
  
  高伸缩性的场景
  MongoDB 非常适合高伸缩性的场景，它是可扩展性的表结构。基于这点，可以将预期范围内，表结构可能会不断扩展的 MySQL 表结构，通过 MongoDB 来存储，这就可以保证表结构的扩展性。
  
  日志系统的场景
  日志系统数据量特别大，如果用 MongoDB 数据库存储这些数据，利用分片集群支持海量数据，同时使用聚集分析和 MapReduce 的能力，是个很好的选择。
  
  分布式文件存储
  MongoDB 还适合存储大尺寸的数据，之前介绍的 GridFS 存储方案，就是基于 MongoDB 的分布式文件存储系统
  
  它在类似于 JSON 的文档中存储数据（使用 BSON，一个 JSON 的二进制版本），存储数据的方式是使用键/值对
  
  面向文档的数据库
  
  支持查询中的正则表达式
  MongoDB 查询结果存储在提供过滤、聚合和排序等一系列功能的游标中，包括 limit()、skip()、 sort()、count()、 distinct() 和 group()。
  高级聚合的 map/reduce 实现
  使用 GridFS 的大文件存储
  类似于 RDBMS 的属性索引支持，您可以直接在文档的选定属性上创建索引
  使用提示、解释计划和分析的查询优化特性
  类似于 MySQL 的主/从复制
  基于集合的对象存储，在需要规范化数据时允许参考查询
  通过自动分片功能水平扩展
  高性能无争用并发机制的即时更新
  
  （_id 属性是唯一标识符，与您的结果可能会不同）： { "_id" : ObjectId("4cfa43ff528bad4e29beec57"), "name" : "red", "value" : "FF0000" }.
  
  MongoDB 支持各种条件运算符，包括：
  
  $lt （小于）
  $lte （小于等于）
  $gt （大于）
  $gte （大于等于）
  $all （匹配数组中的所有值）
  $exists （检查字段是否存在）
  $mod （模数）
  $ne （不等）
  $in （匹配数组一个或多个值）
  $nin （匹配数组中的零值）
  $or （匹配一个或另一个查询）
  $nor （不匹配查询）
  $size （匹配具有预定数量元素的任何数组）
  $type （匹配具有指定 BSON 数据类型的值）
  $not （不等于）
  
  索引
  MongoDB 索引与关系数据库中的索引十分相似。您可以基于任何属性建立索引。此外，索引后的字段可以是任何数据类型，包括一个对象或数组。与 RDBMS 索引相似，可以使用多个属性创建复合索引，也可创建唯一索引，确保不存在重复的值。
  
  要创建一个基本索引，使用 ensureIndex 函数。下面使用字母表集合中的 code 和 char 属性创建一个索引
  
  创建索引
  > db.alphabet.ensureIndex({code: 1});
  > db.alphabet.ensureIndex({char: 1});
  
  分片
  数据库基础架构的一个重要部分就是确保其良好的可扩展性。MongoDB 实现采用一种自动分片机制来确保其横向扩展，这使得 MongoDB 配置可扩展至数千个节点，具有自动负载平衡、无单点故障和自动故障转移功能，向 MongoDB 集群添加新机器也非常简单。
  
  MongoDB 的自动分片特性的好处是它使得从单一服务器转向分片集群变得非常容易，通过无需或很少需要对所需的程序代码进行改动。有关自动分片的工作原理及如何实现它的详细信息，请参阅 MongoDB 文档。
  
  复制
  为了实现故障转移和冗余，MongoDB 在主从配置中提供了复制特性（类似于 MySQL），从而确保节点之间的高度一致性。也就是说，MongoDB 可以在任何时候使用副本集将某个节点定义为主节点，在故障时另一节点担负起主节点的任务。
  
  与 CouchDB 使用复制作为扩展机制的思路不同，MongoDB 主要使用复制来确保高度可用性，方法是使用从属节点作为冗余副本。
  
  有关 MongoDB 复制的更多信息，请参阅文档（参见参考资料中的链接）。
  
  使用 GridFS 的大文件存储
  MongoDB 数据库以 BSON 文档存储数据。BSON 文档的最大大小是 4MB，这不适合存储大文件和对象。MongoDB 通过将文件划分为多个文档之间的较小块，使用 GridFS 规范来存储大文件。
  
  标准 MongoDB 发行版包含将 GridFS 文件添加到本地文件系统以及从本地文件系统检索 GridFS 文件的命令行工具。另外，所有官方 MongoDB API 驱动程序都包含对 GridFS 的支持。有关详细信息，请参阅 MongoDB 文档
  ```

### 缓存使用

- Redis 有哪些类型

  ```
  Redis支持五种数据类型：string（字符串），hash（哈希），list（列表），set（集合）及zset(sorted set：有序集合)。
  ```

  | 类型                 | 简介                                                   | 特性                                                         | 场景                                                         |
  | :------------------- | :----------------------------------------------------- | :----------------------------------------------------------- | :----------------------------------------------------------- |
  | String(字符串)       | 二进制安全                                             | 可以包含任何数据,比如jpg图片或者序列化的对象,一个键最大能存储512M | ---                                                          |
  | Hash(字典)           | 键值对集合,即编程语言中的Map类型                       | 适合存储对象,并且可以像数据库中update一个属性一样只修改某一项属性值(Memcached中需要取出整个字符串反序列化成对象修改完再序列化存回去) | 存储、读取、修改用户属性                                     |
  | List(列表)           | 链表(双向链表)                                         | 增删快,提供了操作某一段元素的API                             | 1,最新消息排行等功能(比如朋友圈的时间线) 2,消息队列          |
  | Set(集合)            | 哈希表实现,元素不重复                                  | 1、添加、删除,查找的复杂度都是O(1) 2、为集合提供了求交集、并集、差集等操作 | 1、共同好友 2、利用唯一性,统计访问网站的所有独立ip 3、好友推荐时,根据tag求交集,大于某个阈值就可以推荐 |
  | Sorted Set(有序集合) | 将Set中的元素增加一个权重参数score,元素按score有序排列 | 数据插入集合时,已经进行天然排序                              | 1、排行榜 2、带权重的消息队列                                |

- Redis 内部结构

- [Redis 内存淘汰机制](https://link.jianshu.com?t=http%3A%2F%2Fblog.720ui.com%2F2016%2Fredis_action_02_maxmemory_policy%2F)

  ```
  1. 客户端发起了需要申请更多内存的命令（如set）。
  2. Redis检查内存使用情况，如果已使用的内存大于maxmemory则开始根据用户配置的不同淘汰策略来淘汰内存（key），从而换取一定的内存。
  3. 如果上面都没问题，则这个命令执行成功
  
  在 Redis 中，允许用户设置最大使用内存大小 server.maxmemory，在内存限定的情况下是很有用的。譬如，在一台 8G 机子上部署了 4 个 Redis 服务点，每一个服务点分配 1G 的内存大小，减少内存紧张的情况，由此获取更为稳健的服务。Redis 内存数据集大小上升到一定大小的时候，就会施行数据淘汰策略。Redis 提供 6 种数据淘汰策略：
  
  volatile-lru：从已设置过期时间的数据集（server.db[i].expires）中挑选最近最少使用 的数据淘汰
  volatile-ttl：从已设置过期时间的数据集（server.db[i].expires）中挑选将要过期的数 据淘汰
  volatile-random：从已设置过期时间的数据集（server.db[i].expires）中任意选择数据 淘汰
  allkeys-lru：从数据集（server.db[i].dict）中挑选最近最少使用的数据淘汰
  allkeys-random：从数据集（server.db[i].dict）中任意选择数据淘汰
  no-enviction（驱逐）：禁止驱逐数据
  
  ```

- [聊聊 Redis 使用场景](https://link.jianshu.com?t=http%3A%2F%2Fblog.720ui.com%2F2017%2Fredis_core_use%2F)

- [Redis 持久化机制](https://link.jianshu.com?t=http%3A%2F%2Fblog.720ui.com%2F2016%2Fredis_action_03_rdb_aof%2F)

- [Redis 集群方案与实现](https://link.jianshu.com?t=http%3A%2F%2Fblog.720ui.com%2F2016%2Fredis_action_04_cluster%2F)

  ```
  1 .redis 安装及配置
    1.1 redis 单点
      1.1.2 在命令窗口操作redis
      1.1.3 使用jedis客户端操作redis
      1.1.4 使用spring-redis操作
      1.1.5 使用Lettuce操作redis
    1.2 redis 主从
    1.3 哨兵sentinel
      1.3.2 哨兵sentinel配置
      1.3.3 启动哨兵，使用jedis连接哨兵操作redis
      1.3.4 编写程序&运行
      1.3.5模拟主节点宕机情况
    1.4 redis cluster
      1.4.1 配置 redis cluster 集群
      1.4.2启动redis集群
      1.4.3 使用jedis连接redis cluster 集群
    1.5 总结
   
   redis主从：是备份关系， 我们操作主库，数据也会同步到从库。 如果主库机器坏了，从库可以上。就好比你 D盘的片丢了，但是你移动硬盘里边备份有。
  redis哨兵：哨兵保证的是HA，保证特殊情况故障自动切换，哨兵盯着你的“redis主从集群”，如果主库死了，它会告诉你新的老大是谁。
  redis集群：集群保证的是高并发，因为多了一些兄弟帮忙一起扛。同时集群会导致数据的分散，整个redis集群会分成一堆数据槽，即不同的key会放到不不同的槽中。
  
  # Jedis读取单点
  Jedis jedis = new Jedis("localhost",6379);
  
  jedis.set("hello", "world");
  
  String value = jedis.get("hello");
  
  System.out.println(value); // get world
  
  jedis.del("hello");
  
  System.out.println(jedis.get("hello"));// get null
  
  # Jedis读取主从
  Jedis jedis_M = new Jedis("192.168.248.129",6379);//主机
          Jedis jedis_S = new Jedis("192.168.248.129",6380);//从机
          
          //遵循“配从不配主”的模式
          jedis_S.slaveof("192.168.248.129",6379);
      
          jedis_M.set("class", "8888");//主机去写
          
          //内存中读写太快，防止读在写之前先完成而出现null的情况，这里做一下延迟
          Thread.sleep(2000);
          
          String result = jedis_S.get("class");//从机去读
          System.out.println(result);
   # Jedis读取集群 哨兵模式
   
    Set<String> hosts = new HashSet<>();
          hosts.add("127.0.0.1:26379");
          //hosts.add("127.0.0.1:36379"); 配置多个哨兵
         
          JedisSentinelPool pool = new JedisSentinelPool("mymaster",hosts);
          Jedis jedis = null;
  
          for(int i=0 ;i<20;i++){
              Thread.sleep(2000);
  
              try{
  
                  jedis = pool.getResource();
                  String v = randomString();
                  jedis.set("hello",v);
  
                  System.out.println(v+"-->"+jedis.get("hello").equals(v));
  
              }catch (Exception e){
                  System.out.println(" [ exception happened]" + e);
              }
  
          }
  # Jedis读取集群 
  
          Set<HostAndPort> jedisClusterNodes = new HashSet<HostAndPort>();
          //Jedis Cluster will attempt to discover cluster nodes automatically
          jedisClusterNodes.add(new HostAndPort("127.0.0.1", 6371));
          jedisClusterNodes.add(new HostAndPort("127.0.0.1", 6372));
          jedisClusterNodes.add(new HostAndPort("127.0.0.1", 6373));
          jedisClusterNodes.add(new HostAndPort("127.0.0.1", 6374));
          jedisClusterNodes.add(new HostAndPort("127.0.0.1", 6375));
          jedisClusterNodes.add(new HostAndPort("127.0.0.1", 6376));
          JedisCluster jc = new JedisCluster(jedisClusterNodes);
          jc.set("foo", "bar");
          String value = jc.get("foo");
          System.out.println(" ===> " + value);
  ```

  

- Redis 云上方案

  ```
  阿里云： 标准版 集群版 读写分离版 性能增强版
  azure： 单机最大 53gb， 120gb  集群
  ```

- Redis持久化

  ```
  Redis提供了RDB持久化和AOF持久化
  RDB持久化是指在指定的时间间隔内将内存中的数据集快照写入磁盘。也是默认的持久化方式，这种方式是就是将内存中数据以快照的方式写入到二进制文件中,默认的文件名为dump.rdb
  AOF文件保存过程
  redis会将每一个收到的写命令都通过write函数追加到文件中(默认是 appendonly.aof)。
  ```

- Redis 为什么是单线程的

- 缓存崩溃

- 缓存降级

- [使用缓存的合理性问题](https://link.jianshu.com?t=http%3A%2F%2Fblog.720ui.com%2F2016%2Fredis_action_01_use_core%2F)

  ## Redis 基础、高级特性与性能调优

  kelgon [匠心零度](javascript:void(0);) *4 days ago*

  点击上方“匠心零度”，选择“设为星标”

  做积极的人，而不是积极废人！

  ![img](https://mmbiz.qpic.cn/mmbiz_jpg/1QxwhpDy7ia2MAPRTKGHHpOicmQGw42Zo6paCrdMbMuMXg34vDtyBQHWMa0NYoqNYeJvariaJb9u5uuWK6Svsvh4A/640?wx_fmt=jpeg&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

  来源：https://www.jianshu.com/p/2f14bc570563

  

  本文将从Redis的基本特性入手，通过讲述Redis的数据结构和主要命令对Redis的基本能力进行直观介绍。之后概览Redis提供的高级能力，并在部署、维护、性能调优等多个方面进行更深入的介绍和指导。

  
  本文适合使用Redis的普通开发人员，以及对Redis进行选型、架构设计和性能调优的架构设计人员。

  

  ## **目录**

  

  - 概述
  - Redis的数据结构和相关常用命令
  - 数据持久化
  - 内存管理与数据淘汰机制
  - Pipelining
  - 事务与Scripting
  - Redis性能调优
  - 主从复制与集群分片
  - Redis Java客户端的选择

  ## 

  ## 

  ## **概述**

  

  Redis是一个开源的，基于内存的结构化数据存储媒介，可以作为数据库、缓存服务或消息服务使用。

  
  Redis支持多种数据结构，包括字符串、哈希表、链表、集合、有序集合、位图、Hyperloglogs等。

  
  Redis具备LRU淘汰、事务实现、以及不同级别的硬盘持久化等能力，并且支持副本集和通过Redis Sentinel实现的高可用方案，同时还支持通过Redis Cluster实现的数据自动分片能力。

  

  Redis的主要功能都基于单线程模型实现，也就是说Redis使用一个线程来服务所有的客户端请求，同时Redis采用了非阻塞式IO，并精细地优化各种命令的算法时间复杂度，这些信息意味着：

  

  - Redis是线程安全的（因为只有一个线程），其所有操作都是原子的，不会因并发产生数据异常
  - Redis的速度非常快（因为使用非阻塞式IO，且大部分命令的算法时间复杂度都是O(1))
  - 使用高耗时的Redis命令是很危险的，会占用唯一的一个线程的大量处理时间，导致所有的请求都被拖慢。（例如时间复杂度为O(N)的KEYS命令，严格禁止在生产环境中使用）

  ## 

  ## 

  ## **Redis的数据结构和相关常用命令**

  

  本节中将介绍Redis支持的主要数据结构，以及相关的常用Redis命令。本节只对Redis命令进行扼要的介绍，且只列出了较常用的命令。如果想要了解完整的Redis命令集，或了解某个命令的详细使用方法，请参考官方文档：

  https://redis.io/commands

  ### 

  ### **Key**

  

  Redis采用Key-Value型的基本数据结构，任何二进制序列都可以作为Redis的Key使用（例如普通的字符串或一张JPEG图片）

  
  关于Key的一些注意事项：

  

  - 不要使用过长的Key。例如使用一个1024字节的key就不是一个好主意，不仅会消耗更多的内存，还会导致查找的效率降低
  - Key短到缺失了可读性也是不好的，例如”u1000flw”比起”user:1000:followers”来说，节省了寥寥的存储空间，却引发了可读性和可维护性上的麻烦
  - 最好使用统一的规范来设计Key，比如”object-type:id:attr”，以这一规范设计出的Key可能是”user:1000″或”comment:1234:reply-to”
  - Redis允许的最大Key长度是512MB（对Value的长度限制也是512MB）

  ### 

  ### **String**

  

  String是Redis的基础数据类型，Redis没有Int、Float、Boolean等数据类型的概念，所有的基本类型在Redis中都以String体现。

  

  与String相关的常用命令：

  

  - SET：为一个key设置value，可以配合EX/PX参数指定key的有效期，通过NX/XX参数针对key是否存在的情况进行区别操作，时间复杂度O(1)
  - GET：获取某个key对应的value，时间复杂度O(1)
  - GETSET：为一个key设置value，并返回该key的原value，时间复杂度O(1)
  - MSET：为多个key设置value，时间复杂度O(N)
  - MSETNX：同MSET，如果指定的key中有任意一个已存在，则不进行任何操作，时间复杂度O(N)
  - MGET：获取多个key对应的value，时间复杂度O(N)

  

  上文提到过，Redis的基本数据类型只有String，但Redis可以把String作为整型或浮点型数字来使用，主要体现在INCR、DECR类的命令上：

  

  - INCR：将key对应的value值自增1，并返回自增后的值。只对可以转换为整型的String数据起作用。时间复杂度O(1)
  - INCRBY：将key对应的value值自增指定的整型数值，并返回自增后的值。只对可以转换为整型的String数据起作用。时间复杂度O(1)
  - DECR/DECRBY：同INCR/INCRBY，自增改为自减。

  

  INCR/DECR系列命令要求操作的value类型为String，并可以转换为64位带符号的整型数字，否则会返回错误。

  
  也就是说，进行INCR/DECR系列命令的value，必须在[-2^63 ~ 2^63 – 1]范围内。

  前文提到过，Redis采用单线程模型，天然是线程安全的，这使得INCR/DECR命令可以非常便利的实现高并发场景下的精确控制。

  

  #### 例1：库存控制

  

  在高并发场景下实现库存余量的精准校验，确保不出现超卖的情况。

  设置库存总量：

  

  > SET inv:remain "100"

   

  库存扣减+余量校验：

  

  > DECR inv:remain

   

  当DECR命令返回值大于等于0时，说明库存余量校验通过，如果返回小于0的值，则说明库存已耗尽。

  

  假设同时有300个并发请求进行库存扣减，Redis能够确保这300个请求分别得到99到-200的返回值，每个请求得到的返回值都是唯一的，绝对不会找出现两个请求得到一样的返回值的情况。

  

  例2：自增序列生成

  

  实现类似于RDBMS的Sequence功能，生成一系列唯一的序列号

  

  设置序列起始值：

  

  > SET sequence "10000"

   

  获取一个序列值：

  

  > INCR sequence

   

  直接将返回值作为序列使用即可。

  

  获取一批（如100个）序列值：

  

  > INCRBY sequence 100

   

  假设返回值为N，那么[N – 99 ~ N]的数值都是可用的序列值。

  

  当多个客户端同时向Redis申请自增序列时，Redis能够确保每个客户端得到的序列值或序列范围都是全局唯一的，绝对不会出现不同客户端得到了重复的序列值的情况。

  

  ### **List**

  

  Redis的List是链表型的数据结构，可以使用LPUSH/RPUSH/LPOP/RPOP等命令在List的两端执行插入元素和弹出元素的操作。虽然List也支持在特定index上插入和读取元素的功能，但其时间复杂度较高（O(N)），应小心使用。

  

  与List相关的常用命令：

  

  - LPUSH：向指定List的左侧（即头部）插入1个或多个元素，返回插入后的List长度。时间复杂度O(N)，N为插入元素的数量
  - RPUSH：同LPUSH，向指定List的右侧（即尾部）插入1或多个元素
  - LPOP：从指定List的左侧（即头部）移除一个元素并返回，时间复杂度O(1)
  - RPOP：同LPOP，从指定List的右侧（即尾部）移除1个元素并返回
  - LPUSHX/RPUSHX：与LPUSH/RPUSH类似，区别在于，LPUSHX/RPUSHX操作的key如果不存在，则不会进行任何操作
  - LLEN：返回指定List的长度，时间复杂度O(1)
  - LRANGE：返回指定List中指定范围的元素（双端包含，即LRANGE key 0 10会返回11个元素），时间复杂度O(N)。应尽可能控制一次获取的元素数量，一次获取过大范围的List元素会导致延迟，同时对长度不可预知的List，避免使用LRANGE key 0 -1这样的完整遍历操作。

  

  应谨慎使用的List相关命令：

  

  - LINDEX：返回指定List指定index上的元素，如果index越界，返回nil。index数值是回环的，即-1代表List最后一个位置，-2代表List倒数第二个位置。时间复杂度O(N)
  - LSET：将指定List指定index上的元素设置为value，如果index越界则返回错误，时间复杂度O(N)，如果操作的是头/尾部的元素，则时间复杂度为O(1)
  - LINSERT：向指定List中指定元素之前/之后插入一个新元素，并返回操作后的List长度。如果指定的元素不存在，返回-1。如果指定key不存在，不会进行任何操作，时间复杂度O(N)

  

  由于Redis的List是链表结构的，上述的三个命令的算法效率较低，需要对List进行遍历，命令的耗时无法预估，在List长度大的情况下耗时会明显增加，应谨慎使用。

  

  换句话说，Redis的List实际是设计来用于实现队列，而不是用于实现类似ArrayList这样的列表的。如果你不是想要实现一个双端出入的队列，那么请尽量不要使用Redis的List数据结构。

  

  为了更好支持队列的特性，Redis还提供了一系列阻塞式的操作命令，如BLPOP/BRPOP等，能够实现类似于BlockingQueue的能力，即在List为空时，阻塞该连接，直到List中有对象可以出队时再返回。针对阻塞类的命令，此处不做详细探讨，请参考官方文档（https://redis.io/topics/data-types-intro） 中”Blocking operations on lists”一节。

  

  ### **Hash**

  

  Hash即哈希表，Redis的Hash和传统的哈希表一样，是一种field-value型的数据结构，可以理解成将HashMap搬入Redis。

  
  Hash非常适合用于表现对象类型的数据，用Hash中的field对应对象的field即可。

  
  Hash的优点包括：

  

  - 可以实现二元查找，如”查找ID为1000的用户的年龄”
  - 比起将整个对象序列化后作为String存储的方法，Hash能够有效地减少网络传输的消耗
  - 当使用Hash维护一个集合时，提供了比List效率高得多的随机访问命令

  

  与Hash相关的常用命令：

  

  - HSET：将key对应的Hash中的field设置为value。如果该Hash不存在，会自动创建一个。时间复杂度O(1)
  - HGET：返回指定Hash中field字段的值，时间复杂度O(1)
  - HMSET/HMGET：同HSET和HGET，可以批量操作同一个key下的多个field，时间复杂度：O(N)，N为一次操作的field数量
  - HSETNX：同HSET，但如field已经存在，HSETNX不会进行任何操作，时间复杂度O(1)
  - HEXISTS：判断指定Hash中field是否存在，存在返回1，不存在返回0，时间复杂度O(1)
  - HDEL：删除指定Hash中的field（1个或多个），时间复杂度：O(N)，N为操作的field数量
  - HINCRBY：同INCRBY命令，对指定Hash中的一个field进行INCRBY，时间复杂度O(1)

  

  应谨慎使用的Hash相关命令：

  

  - HGETALL：返回指定Hash中所有的field-value对。返回结果为数组，数组中field和value交替出现。时间复杂度O(N)
  - HKEYS/HVALS：返回指定Hash中所有的field/value，时间复杂度O(N)

  

  上述三个命令都会对Hash进行完整遍历，Hash中的field数量与命令的耗时线性相关，对于尺寸不可预知的Hash，应严格避免使用上面三个命令，而改为使用HSCAN命令进行游标式的遍历，具体请见 

  https://redis.io/commands/scan

  ### 

  ### **Set**

  

  Redis Set是无序的，不可重复的String集合。

  

  与Set相关的常用命令：

  

  - SADD：向指定Set中添加1个或多个member，如果指定Set不存在，会自动创建一个。时间复杂度O(N)，N为添加的member个数
  - SREM：从指定Set中移除1个或多个member，时间复杂度O(N)，N为移除的member个数
  - SRANDMEMBER：从指定Set中随机返回1个或多个member，时间复杂度O(N)，N为返回的member个数
  - SPOP：从指定Set中随机移除并返回count个member，时间复杂度O(N)，N为移除的member个数
  - SCARD：返回指定Set中的member个数，时间复杂度O(1)
  - SISMEMBER：判断指定的value是否存在于指定Set中，时间复杂度O(1)
  - SMOVE：将指定member从一个Set移至另一个Set

  

  慎用的Set相关命令：

  

  - SMEMBERS：返回指定Hash中所有的member，时间复杂度O(N)
  - SUNION/SUNIONSTORE：计算多个Set的并集并返回/存储至另一个Set中，时间复杂度O(N)，N为参与计算的所有集合的总member数
  - SINTER/SINTERSTORE：计算多个Set的交集并返回/存储至另一个Set中，时间复杂度O(N)，N为参与计算的所有集合的总member数
  - SDIFF/SDIFFSTORE：计算1个Set与1或多个Set的差集并返回/存储至另一个Set中，时间复杂度O(N)，N为参与计算的所有集合的总member数

  

  上述几个命令涉及的计算量大，应谨慎使用，特别是在参与计算的Set尺寸不可知的情况下，应严格避免使用。可以考虑通过SSCAN命令遍历获取相关Set的全部member（具体请见 https://redis.io/commands/scan ），如果需要做并集/交集/差集计算，可以在客户端进行，或在不服务实时查询请求的Slave上进行。

  

  ### **Sorted Set**

  

  Redis Sorted Set是有序的、不可重复的String集合。Sorted Set中的每个元素都需要指派一个分数(score)，Sorted Set会根据score对元素进行升序排序。如果多个member拥有相同的score，则以字典序进行升序排序。

  

  Sorted Set非常适合用于实现排名。

  

  Sorted Set的主要命令：

  

  - ZADD：向指定Sorted Set中添加1个或多个member，时间复杂度O(Mlog(N))，M为添加的member数量，N为Sorted Set中的member数量
  - ZREM：从指定Sorted Set中删除1个或多个member，时间复杂度O(Mlog(N))，M为删除的member数量，N为Sorted Set中的member数量
  - ZCOUNT：返回指定Sorted Set中指定score范围内的member数量，时间复杂度：O(log(N))
  - ZCARD：返回指定Sorted Set中的member数量，时间复杂度O(1)
  - ZSCORE：返回指定Sorted Set中指定member的score，时间复杂度O(1)
  - ZRANK/ZREVRANK：返回指定member在Sorted Set中的排名，ZRANK返回按升序排序的排名，ZREVRANK则返回按降序排序的排名。时间复杂度O(log(N))
  - ZINCRBY：同INCRBY，对指定Sorted Set中的指定member的score进行自增，时间复杂度O(log(N))

  

  慎用的Sorted Set相关命令：

  

  - ZRANGE/ZREVRANGE：返回指定Sorted Set中指定排名范围内的所有member，ZRANGE为按score升序排序，ZREVRANGE为按score降序排序，时间复杂度O(log(N)+M)，M为本次返回的member数
  - ZRANGEBYSCORE/ZREVRANGEBYSCORE：返回指定Sorted Set中指定score范围内的所有member，返回结果以升序/降序排序，min和max可以指定为-inf和+inf，代表返回所有的member。时间复杂度O(log(N)+M)
  - ZREMRANGEBYRANK/ZREMRANGEBYSCORE：移除Sorted Set中指定排名范围/指定score范围内的所有member。时间复杂度O(log(N)+M)

  

  上述几个命令，应尽量避免传递[0 -1]或[-inf +inf]这样的参数，来对Sorted Set做一次性的完整遍历，特别是在Sorted Set的尺寸不可预知的情况下。可以通过ZSCAN命令来进行游标式的遍历（具体请见 https://redis.io/commands/scan ），或通过LIMIT参数来限制返回member的数量（适用于ZRANGEBYSCORE和ZREVRANGEBYSCORE命令），以实现游标式的遍历。

  

  ### Bitmap和HyperLogLog

  

  Redis的这两种数据结构相较之前的并不常用，在本文中只做简要介绍，如想要详细了解这两种数据结构与其相关的命令，请参考官方文档

  https://redis.io/topics/data-types-intro 中的相关章节

  

  Bitmap在Redis中不是一种实际的数据类型，而是一种将String作为Bitmap使用的方法。可以理解为将String转换为bit数组。使用Bitmap来存储true/false类型的简单数据极为节省空间。

  

  HyperLogLogs是一种主要用于数量统计的数据结构，它和Set类似，维护一个不可重复的String集合，但是HyperLogLogs并不维护具体的member内容，只维护member的个数。也就是说，HyperLogLogs只能用于计算一个集合中不重复的元素数量，所以它比Set要节省很多内存空间。

  

  ### 其他常用命令

  

  - EXISTS：判断指定的key是否存在，返回1代表存在，0代表不存在，时间复杂度O(1)
  - DEL：删除指定的key及其对应的value，时间复杂度O(N)，N为删除的key数量
  - EXPIRE/PEXPIRE：为一个key设置有效期，单位为秒或毫秒，时间复杂度O(1)
  - TTL/PTTL：返回一个key剩余的有效时间，单位为秒或毫秒，时间复杂度O(1)
  - RENAME/RENAMENX：将key重命名为newkey。使用RENAME时，如果newkey已经存在，其值会被覆盖；使用RENAMENX时，如果newkey已经存在，则不会进行任何操作，时间复杂度O(1)
  - TYPE：返回指定key的类型，string, list, set, zset, hash。时间复杂度O(1)
  - CONFIG GET：获得Redis某配置项的当前值，可以使用*通配符，时间复杂度O(1)
  - CONFIG SET：为Redis某个配置项设置新值，时间复杂度O(1)
  - CONFIG REWRITE：让Redis重新加载redis.conf中的配置

  ## 

  ## 

  ## **数据持久化**

  

  Redis提供了将数据定期自动持久化至硬盘的能力，包括RDB和AOF两种方案，两种方案分别有其长处和短板，可以配合起来同时运行，确保数据的稳定性。

  

  ### **必须使用数据持久化吗？**

  

  Redis的数据持久化机制是可以关闭的。如果你只把Redis作为缓存服务使用，Redis中存储的所有数据都不是该数据的主体而仅仅是同步过来的备份，那么可以关闭Redis的数据持久化机制。

  
  但通常来说，仍然建议至少开启RDB方式的数据持久化，因为：

  

  - RDB方式的持久化几乎不损耗Redis本身的性能，在进行RDB持久化时，Redis主进程唯一需要做的事情就是fork出一个子进程，所有持久化工作都由子进程完成
  - Redis无论因为什么原因crash掉之后，重启时能够自动恢复到上一次RDB快照中记录的数据。这省去了手工从其他数据源（如DB）同步数据的过程，而且要比其他任何的数据恢复方式都要快
  - 现在硬盘那么大，真的不缺那一点地方

  ### 

  ### **RDB**

  

  采用RDB持久方式，Redis会定期保存数据快照至一个rbd文件中，并在启动时自动加载rdb文件，恢复之前保存的数据。可以在配置文件中配置Redis进行快照保存的时机：

  

  > save [seconds] [changes]

   

  意为在[seconds]秒内如果发生了[changes]次数据修改，则进行一次RDB快照保存，例如

  

  > save 60 100

   

  会让Redis每60秒检查一次数据变更情况，如果发生了100次或以上的数据变更，则进行RDB快照保存。

  

  可以配置多条save指令，让Redis执行多级的快照保存策略。

  

  Redis默认开启RDB快照，默认的RDB策略如下：

  

  > save 900 1
  >
  > save 300 10
  >
  > save 60 10000

  

  也可以通过BGSAVE命令手工触发RDB快照保存。

  

  RDB的优点：

  

  - 对性能影响最小。如前文所述，Redis在保存RDB快照时会fork出子进程进行，几乎不影响Redis处理客户端请求的效率。
  - 每次快照会生成一个完整的数据快照文件，所以可以辅以其他手段保存多个时间点的快照（例如把每天0点的快照备份至其他存储媒介中），作为非常可靠的灾难恢复手段。
  - 使用RDB文件进行数据恢复比使用AOF要快很多。

  

  RDB的缺点：

  

  - 快照是定期生成的，所以在Redis crash时或多或少会丢失一部分数据。
  - 如果数据集非常大且CPU不够强（比如单核CPU），Redis在fork子进程时可能会消耗相对较长的时间（长至1秒），影响这期间的客户端请求。

  ### 

  ### **AOF**

  

  采用AOF持久方式时，Redis会把每一个写请求都记录在一个日志文件里。在Redis重启时，会把AOF文件中记录的所有写操作顺序执行一遍，确保数据恢复到最新。

  

  AOF默认是关闭的，如要开启，进行如下配置：

  

  > appendonly yes

   

  AOF提供了三种fsync配置，always/everysec/no，通过配置项[appendfsync]指定：

  

  - appendfsync no：不进行fsync，将flush文件的时机交给OS决定，速度最快
  - appendfsync always：每写入一条日志就进行一次fsync操作，数据安全性最高，但速度最慢
  - appendfsync everysec：折中的做法，交由后台线程每秒fsync一次

  

  随着AOF不断地记录写操作日志，必定会出现一些无用的日志，例如某个时间点执行了命令SET key1 “abc”，在之后某个时间点又执行了SET key1 “bcd”，那么第一条命令很显然是没有用的。大量的无用日志会让AOF文件过大，也会让数据恢复的时间过长。

  
  所以Redis提供了AOF rewrite功能，可以重写AOF文件，只保留能够把数据恢复到最新状态的最小写操作集。

  
  AOF rewrite可以通过BGREWRITEAOF命令触发，也可以配置Redis定期自动进行：

  

  > auto-aof-rewrite-percentage 100
  >
  > auto-aof-rewrite-min-size 64mb

  

  上面两行配置的含义是，Redis在每次AOF rewrite时，会记录完成rewrite后的AOF日志大小，当AOF日志大小在该基础上增长了100%后，自动进行AOF rewrite。同时如果增长的大小没有达到64mb，则不会进行rewrite。

  

  AOF的优点：

  

  - 最安全，在启用appendfsync always时，任何已写入的数据都不会丢失，使用在启用appendfsync everysec也至多只会丢失1秒的数据。
  - AOF文件在发生断电等问题时也不会损坏，即使出现了某条日志只写入了一半的情况，也可以使用redis-check-aof工具轻松修复。
  - AOF文件易读，可修改，在进行了某些错误的数据清除操作后，只要AOF文件没有rewrite，就可以把AOF文件备份出来，把错误的命令删除，然后恢复数据。

  

  AOF的缺点：

  

  - AOF文件通常比RDB文件更大
  - 性能消耗比RDB高
  - 数据恢复速度比RDB慢

  ## 

  ## 

  ## **内存管理与数据淘汰机制**

  

  ### **最大内存设置**

  

  默认情况下，在32位OS中，Redis最大使用3GB的内存，在64位OS中则没有限制。

  在使用Redis时，应该对数据占用的最大空间有一个基本准确的预估，并为Redis设定最大使用的内存。否则在64位OS中Redis会无限制地占用内存（当物理内存被占满后会使用swap空间），容易引发各种各样的问题。

  

  通过如下配置控制Redis使用的最大内存：

  

  > maxmemory 100mb

   

  在内存占用达到了maxmemory后，再向Redis写入数据时，Redis会：

  

  - 根据配置的数据淘汰策略尝试淘汰数据，释放空间
  - 如果没有数据可以淘汰，或者没有配置数据淘汰策略，那么Redis会对所有写请求返回错误，但读请求仍然可以正常执行

  

  在为Redis设置maxmemory时，需要注意：

  

  - 如果采用了Redis的主从同步，主节点向从节点同步数据时，会占用掉一部分内存空间，如果maxmemory过于接近主机的可用内存，导致数据同步时内存不足。所以设置的maxmemory不要过于接近主机可用的内存，留出一部分预留用作主从同步。

  ### 

  ### 

  ### **数据淘汰机制**

  

  Redis提供了5种数据淘汰策略：

  

  - volatile-lru：使用LRU算法进行数据淘汰（淘汰上次使用时间最早的，且使用次数最少的key），只淘汰设定了有效期的key
  - allkeys-lru：使用LRU算法进行数据淘汰，所有的key都可以被淘汰
  - volatile-random：随机淘汰数据，只淘汰设定了有效期的key
  - allkeys-random：随机淘汰数据，所有的key都可以被淘汰
  - volatile-ttl：淘汰剩余有效期最短的key

  

  最好为Redis指定一种有效的数据淘汰策略以配合maxmemory设置，避免在内存使用满后发生写入失败的情况。

  

  一般来说，推荐使用的策略是volatile-lru，并辨识Redis中保存的数据的重要性。对于那些重要的，绝对不能丢弃的数据（如配置类数据等），应不设置有效期，这样Redis就永远不会淘汰这些数据。对于那些相对不是那么重要的，并且能够热加载的数据（比如缓存最近登录的用户信息，当在Redis中找不到时，程序会去DB中读取），可以设置上有效期，这样在内存不够时Redis就会淘汰这部分数据。

  

  配置方法：

  

  > maxmemory-policy volatile-lru   #默认是noeviction，即不进行数据淘汰

   

  **Pipelining**

  

  **Pipelining**

  

  Redis提供许多批量操作的命令，如MSET/MGET/HMSET/HMGET等等，这些命令存在的意义是减少维护网络连接和传输数据所消耗的资源和时间。

  

  例如连续使用5次SET命令设置5个不同的key，比起使用一次MSET命令设置5个不同的key，效果是一样的，但前者会消耗更多的RTT(Round Trip Time)时长，永远应优先使用后者。

  

  然而，如果客户端要连续执行的多次操作无法通过Redis命令组合在一起，例如：

  

  > SET a "abc"
  >
  > INCR b
  >
  > HSET c name "hi"

  

  此时便可以使用Redis提供的pipelining功能来实现在一次交互中执行多条命令。

  

  使用pipelining时，只需要从客户端一次向Redis发送多条命令（以rn）分隔，Redis就会依次执行这些命令，并且把每个命令的返回按顺序组装在一起一次返回，比如：

  

  > $ (printf "PINGrnPINGrnPINGrn"; sleep 1) | nc localhost 6379
  >
  > +PONG
  >
  > +PONG
  >
  > +PONG

  

  大部分的Redis客户端都对Pipelining提供支持，所以开发者通常并不需要自己手工拼装命令列表。

  

  **Pipelining的局限性**

  

  Pipelining只能用于执行连续且无相关性的命令，当某个命令的生成需要依赖于前一个命令的返回时，就无法使用Pipelining了。

  

  通过Scripting功能，可以规避这一局限性

  

  **事务与Scripting**

  

  Pipelining能够让Redis在一次交互中处理多条命令，然而在一些场景下，我们可能需要在此基础上确保这一组命令是连续执行的。

  

  比如获取当前累计的PV数并将其清0

  

  > \> GET vCount
  >
  > 12384
  >
  > \> SET vCount 0
  >
  > OK

  

  如果在GET和SET命令之间插进来一个INCR vCount，就会使客户端拿到的vCount不准确。

  

  Redis的事务可以确保复数命令执行时的原子性。也就是说Redis能够保证：一个事务中的一组命令是绝对连续执行的，在这些命令执行完成之前，绝对不会有来自于其他连接的其他命令插进去执行。

  

  通过MULTI和EXEC命令来把这两个命令加入一个事务中：

  

  > \> MULTI
  >
  > OK
  >
  > \> GET vCount
  >
  > QUEUED
  >
  > \> SET vCount 0
  >
  > QUEUED
  >
  > \> EXEC
  >
  > 1) 12384
  >
  > 2) OK

  

  Redis在接收到MULTI命令后便会开启一个事务，这之后的所有读写命令都会保存在队列中但并不执行，直到接收到EXEC命令后，Redis会把队列中的所有命令连续顺序执行，并以数组形式返回每个命令的返回结果。

  

  可以使用DISCARD命令放弃当前的事务，将保存的命令队列清空。

  

  需要注意的是，Redis事务不支持回滚：

  

  如果一个事务中的命令出现了语法错误，大部分客户端驱动会返回错误，2.6.5版本以上的Redis也会在执行EXEC时检查队列中的命令是否存在语法错误，如果存在，则会自动放弃事务并返回错误。

  

  但如果一个事务中的命令有非语法类的错误（比如对String执行HSET操作），无论客户端驱动还是Redis都无法在真正执行这条命令之前发现，所以事务中的所有命令仍然会被依次执行。在这种情况下，会出现一个事务中部分命令成功部分命令失败的情况，然而与RDBMS不同，Redis不提供事务回滚的功能，所以只能通过其他方法进行数据的回滚。

  

  **通过事务实现CAS**

  

  Redis提供了WATCH命令与事务搭配使用，实现CAS乐观锁的机制。

  

  假设要实现将某个商品的状态改为已售：

  

  > **if**(exec(HGET stock:1001 state) == "in stock")
  >
  > ​    exec(HSET stock:1001 state "sold");

  

  这一伪代码执行时，无法确保并发安全性，有可能多个客户端都获取到了”in stock”的状态，导致一个库存被售卖多次。

  

  使用WATCH命令和事务可以解决这一问题：

  

  > exec(WATCH stock:1001);
  >
  > **if**(exec(HGET stock:1001 state) == "in stock") {
  >
  > ​    exec(MULTI);
  >
  > ​    exec(HSET stock:1001 state "sold");
  >
  > ​    exec(EXEC);
  >
  > }

  

  WATCH的机制是：在事务EXEC命令执行时，Redis会检查被WATCH的key，只有被WATCH的key从WATCH起始时至今没有发生过变更，EXEC才会被执行。如果WATCH的key在WATCH命令到EXEC命令之间发生过变化，则EXEC命令会返回失败。

  

  ### **Scripting**

  

  通过EVAL与EVALSHA命令，可以让Redis执行LUA脚本。这就类似于RDBMS的存储过程一样，可以把客户端与Redis之间密集的读/写交互放在服务端进行，避免过多的数据交互，提升性能。

  

  Scripting功能是作为事务功能的替代者诞生的，事务提供的所有能力Scripting都可以做到。Redis官方推荐使用LUA Script来代替事务，前者的效率和便利性都超过了事务。

  

  关于Scripting的具体使用，本文不做详细介绍，请参考官方文档 

  https://redis.io/commands/eval

  ## 

  ## **Redis性能调优**

  

  尽管Redis是一个非常快速的内存数据存储媒介，也并不代表Redis不会产生性能问题。

  
  前文中提到过，Redis采用单线程模型，所有的命令都是由一个线程串行执行的，所以当某个命令执行耗时较长时，会拖慢其后的所有命令，这使得Redis对每个任务的执行效率更加敏感。

  

  针对Redis的性能优化，主要从下面几个层面入手：

  

  - 最初的也是最重要的，确保没有让Redis执行耗时长的命令
  - 使用pipelining将连续执行的命令组合执行
  - 操作系统的Transparent huge pages功能必须关闭：

  

  > echo never > /sys/kernel/mm/transparent_hugepage/enabled

   

  - 如果在虚拟机中运行Redis，可能天然就有虚拟机环境带来的固有延迟。可以通过./redis-cli –intrinsic-latency 100命令查看固有延迟。同时如果对Redis的性能有较高要求的话，应尽可能在物理机上直接部署Redis。
  - 检查数据持久化策略
  - 考虑引入读写分离机制

  ### 

  ### 

  ### **长耗时命令**

  

  Redis绝大多数读写命令的时间复杂度都在O(1)到O(N)之间，在文本和官方文档中均对每个命令的时间复杂度有说明。

  

  通常来说，O(1)的命令是安全的，O(N)命令在使用时需要注意，如果N的数量级不可预知，则应避免使用。例如对一个field数未知的Hash数据执行HGETALL/HKEYS/HVALS命令，通常来说这些命令执行的很快，但如果这个Hash中的field数量极多，耗时就会成倍增长。

  
  又如使用SUNION对两个Set执行Union操作，或使用SORT对List/Set执行排序操作等时，都应该严加注意。

  

  避免在使用这些O(N)命令时发生问题主要有几个办法：

  

  - 不要把List当做列表使用，仅当做队列来使用
  - 通过机制严格控制Hash、Set、Sorted Set的大小
  - 可能的话，将排序、并集、交集等操作放在客户端执行
  - 绝对禁止使用KEYS命令
  - 避免一次性遍历集合类型的所有成员，而应使用SCAN类的命令进行分批的，游标式的遍历

  

  Redis提供了SCAN命令，可以对Redis中存储的所有key进行游标式的遍历，避免使用KEYS命令带来的性能问题。同时还有SSCAN/HSCAN/ZSCAN等命令，分别用于对Set/Hash/Sorted Set中的元素进行游标式遍历。SCAN类命令的使用请参考官方文档：

  https://redis.io/commands/scan

  

  Redis提供了Slow Log功能，可以自动记录耗时较长的命令。相关的配置参数有两个：

  

  > slowlog-log-slower-than xxxms  #执行时间慢于xxx毫秒的命令计入Slow Log
  >
  > slowlog-max-len xxx  #Slow Log的长度，即最大纪录多少条Slow Log

  

  使用SLOWLOG GET [number]命令，可以输出最近进入Slow Log的number条命令。

  
  使用SLOWLOG RESET命令，可以重置Slow Log

  

  ### **网络引发的延迟**

  

  - 尽可能使用长连接或连接池，避免频繁创建销毁连接
  - 客户端进行的批量数据操作，应使用Pipeline特性在一次交互中完成。具体请参照本文的Pipelining章节

  ### 

  ### **数据持久化引发的延迟**

  

  Redis的数据持久化工作本身就会带来延迟，需要根据数据的安全级别和性能要求制定合理的持久化策略：

  

  - AOF + fsync always的设置虽然能够绝对确保数据安全，但每个操作都会触发一次fsync，会对Redis的性能有比较明显的影响

  - AOF + fsync every second是比较好的折中方案，每秒fsync一次

  - AOF + fsync never会提供AOF持久化方案下的最优性能

  - 使用RDB持久化通常会提供比使用AOF更高的性能，但需要注意RDB的策略配置

  - 每一次RDB快照和AOF Rewrite都需要Redis主进程进行fork操作。fork操作本身可能会产生较高的耗时，与CPU和Redis占用的内存大小有关。根据具体的情况合理配置RDB快照和AOF Rewrite时机，避免过于频繁的fork带来的延迟

    

  > Redis在fork子进程时需要将内存分页表拷贝至子进程，以占用了24GB内存的Redis实例为例，共需要拷贝24GB / 4kB * 8 = 48MB的数据。在使用单Xeon 2.27Ghz的物理机上，这一fork操作耗时216ms。

  > 可以通过INFO命令返回的latest_fork_usec字段查看上一次fork操作的耗时（微秒）

  ### 

  ### 

  ### **Swap引发的延迟**

  

  当Linux将Redis所用的内存分页移至swap空间时，将会阻塞Redis进程，导致Redis出现不正常的延迟。Swap通常在物理内存不足或一些进程在进行大量I/O操作时发生，应尽可能避免上述两种情况的出现。

  

  /proc/<pid>/smaps文件中会保存进程的swap记录，通过查看这个文件，能够判断Redis的延迟是否由Swap产生。如果这个文件中记录了较大的Swap size，则说明延迟很有可能是Swap造成的。

  

  ### **数据淘汰引发的延迟**

  

  当同一秒内有大量key过期时，也会引发Redis的延迟。在使用时应尽量将key的失效时间错开。

  

  ### 引入读写分离机制

  

  Redis的主从复制能力可以实现一主多从的多节点架构，在这一架构下，主节点接收所有写请求，并将数据同步给多个从节点。

  
  在这一基础上，我们可以让从节点提供对实时性要求不高的读请求服务，以减小主节点的压力。

  
  尤其是针对一些使用了长耗时命令的统计类任务，完全可以指定在一个或多个从节点上执行，避免这些长耗时命令影响其他请求的响应。

  

  关于读写分离的具体说明，请参见后续章节

  

  ## **主从复制与集群分片**

  

  ### **主从复制**

  

  Redis支持一主多从的主从复制架构。一个Master实例负责处理所有的写请求，Master将写操作同步至所有Slave。

  
  借助Redis的主从复制，可以实现读写分离和高可用：

  

  - 实时性要求不是特别高的读请求，可以在Slave上完成，提升效率。特别是一些周期性执行的统计任务，这些任务可能需要执行一些长耗时的Redis命令，可以专门规划出1个或几个Slave用于服务这些统计任务
  - 借助Redis Sentinel可以实现高可用，当Master crash后，Redis Sentinel能够自动将一个Slave晋升为Master，继续提供服务

  

  启用主从复制非常简单，只需要配置多个Redis实例，在作为Slave的Redis实例中配置：

  

  > slaveof 192.168.1.1 6379  #指定Master的IP和端口

   

  当Slave启动后，会从Master进行一次冷启动数据同步，由Master触发BGSAVE生成RDB文件推送给Slave进行导入，导入完成后Master再将增量数据通过Redis Protocol同步给Slave。之后主从之间的数据便一直以Redis Protocol进行同步

  

  **使用Sentinel做自动failover**

  

  Redis的主从复制功能本身只是做数据同步，并不提供监控和自动failover能力，要通过主从复制功能来实现Redis的高可用，还需要引入一个组件：Redis Sentinel

  

  Redis Sentinel是Redis官方开发的监控组件，可以监控Redis实例的状态，通过Master节点自动发现Slave节点，并在监测到Master节点失效时选举出一个新的Master，并向所有Redis实例推送新的主从配置。

  

  Redis Sentinel需要至少部署3个实例才能形成选举关系。

  

  关键配置：

  

  ![img](https://mmbiz.qpic.cn/mmbiz_png/DmibiaFiaAI4B1iaicSC4Zib8r1V37W5T80Iaf30fygDzh2BTQJQePnH03E98CibQict0gK7atGAOc5gicW8ibt2LlOzOP8w/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

  

  另外需要注意的是，Redis Sentinel实现的自动failover不是在同一个IP和端口上完成的，也就是说自动failover产生的新Master提供服务的IP和端口与之前的Master是不一样的，所以要实现HA，还要求客户端必须支持Sentinel，能够与Sentinel交互获得新Master的信息才行。

  

  ### **集群分片**

  

  为何要做集群分片：

  

  - Redis中存储的数据量大，一台主机的物理内存已经无法容纳
  - Redis的写请求并发量大，一个Redis实例以无法承载

  

  当上述两个问题出现时，就必须要对Redis进行分片了。

  
  Redis的分片方案有很多种，例如很多Redis的客户端都自行实现了分片功能，也有向Twemproxy这样的以代理方式实现的Redis分片方案。然而首选的方案还应该是Redis官方在3.0版本中推出的Redis Cluster分片方案。

  

  本文不会对Redis Cluster的具体安装和部署细节进行介绍，重点介绍Redis Cluster带来的好处与弊端。

  

  #### **Redis Cluster的能力**

  

  - 能够自动将数据分散在多个节点上
  - 当访问的key不在当前分片上时，能够自动将请求转发至正确的分片
  - 当集群中部分节点失效时仍能提供服务

  

  其中第三点是基于主从复制来实现的，Redis Cluster的每个数据分片都采用了主从复制的结构，原理和前文所述的主从复制完全一致，唯一的区别是省去了Redis Sentinel这一额外的组件，由Redis Cluster负责进行一个分片内部的节点监控和自动failover。

  

  #### **Redis Cluster分片原理**

  

  Redis Cluster中共有16384个hash slot，Redis会计算每个key的CRC16，将结果与16384取模，来决定该key存储在哪一个hash slot中，同时需要指定Redis Cluster中每个数据分片负责的Slot数。Slot的分配在任何时间点都可以进行重新分配。

  

  客户端在对key进行读写操作时，可以连接Cluster中的任意一个分片，如果操作的key不在此分片负责的Slot范围内，Redis Cluster会自动将请求重定向到正确的分片上。

  

  #### **hash tags**

  

  在基础的分片原则上，Redis还支持hash tags功能，以hash tags要求的格式明明的key，将会确保进入同一个Slot中。例如：{uiv}user:1000和{uiv}user:1001拥有同样的hash tag {uiv}，会保存在同一个Slot中。

  

  使用Redis Cluster时，pipelining、事务和LUA Script功能涉及的key必须在同一个数据分片上，否则将会返回错误。如要在Redis Cluster中使用上述功能，就必须通过hash tags来确保一个pipeline或一个事务中操作的所有key都位于同一个Slot中。

  

  > 有一些客户端（如Redisson）实现了集群化的pipelining操作，可以自动将一个pipeline里的命令按key所在的分片进行分组，分别发到不同的分片上执行。但是Redis不支持跨分片的事务，事务和LUA Script还是必须遵循所有key在一个分片上的规则要求。

  ### 

  ### **主从复制 vs 集群分片**

  

  在设计软件架构时，要如何在主从复制和集群分片两种部署方案中取舍呢？

  

  从各个方面看，Redis Cluster都是优于主从复制的方案

  

  - Redis Cluster能够解决单节点上数据量过大的问题
  - Redis Cluster能够解决单节点访问压力过大的问题
  - Redis Cluster包含了主从复制的能力

  

  那是不是代表Redis Cluster永远是优于主从复制的选择呢？

  

  并不是。

  

  软件架构永远不是越复杂越好，复杂的架构在带来显著好处的同时，一定也会带来相应的弊端。采用Redis Cluster的弊端包括：

  

  - 维护难度增加。在使用Redis Cluster时，需要维护的Redis实例数倍增，需要监控的主机数量也相应增加，数据备份/持久化的复杂度也会增加。同时在进行分片的增减操作时，还需要进行reshard操作，远比主从模式下增加一个Slave的复杂度要高。
  - 客户端资源消耗增加。当客户端使用连接池时，需要为每一个数据分片维护一个连接池，客户端同时需要保持的连接数成倍增多，加大了客户端本身和操作系统资源的消耗。
  - 性能优化难度增加。你可能需要在多个分片上查看Slow Log和Swap日志才能定位性能问题。
  - 事务和LUA Script的使用成本增加。在Redis Cluster中使用事务和LUA Script特性有严格的限制条件，事务和Script中操作的key必须位于同一个分片上，这就使得在开发时必须对相应场景下涉及的key进行额外的规划和规范要求。如果应用的场景中大量涉及事务和Script的使用，如何在保证这两个功能的正常运作前提下把数据平均分到多个数据分片中就会成为难点。

  

  所以说，在主从复制和集群分片两个方案中做出选择时，应该从应用软件的功能特性、数据和访问量级、未来发展规划等方面综合考虑，只在确实有必要引入数据分片时再使用Redis Cluster。

  
  下面是一些建议：

  

  1. 需要在Redis中存储的数据有多大？未来2年内可能发展为多大？这些数据是否都需要长期保存？是否可以使用LRU算法进行非热点数据的淘汰？综合考虑前面几个因素，评估出Redis需要使用的物理内存。
  2. 用于部署Redis的主机物理内存有多大？有多少可以分配给Redis使用？对比(1)中的内存需求评估，是否足够用？
  3. Redis面临的并发写压力会有多大？在不使用pipelining时，Redis的写性能可以超过10万次/秒（更多的benchmark可以参考 https://redis.io/topics/benchmarks ）
  4. 在使用Redis时，是否会使用到pipelining和事务功能？使用的场景多不多？

  

  综合上面几点考虑，如果单台主机的可用物理内存完全足以支撑对Redis的容量需求，且Redis面临的并发写压力距离Benchmark值还尚有距离，建议采用主从复制的架构，可以省去很多不必要的麻烦。同时，如果应用中大量使用pipelining和事务，也建议尽可能选择主从复制架构，可以减少设计和开发时的复杂度。

  

  ## **Redis Java客户端的选择**

  

  Redis的Java客户端很多，官方推荐的有三种：Jedis、Redisson和lettuce。

  

  在这里对Jedis和Redisson进行对比介绍

  

  Jedis：

  

  - 轻量，简洁，便于集成和改造
  - 支持连接池
  - 支持pipelining、事务、LUA Scripting、Redis Sentinel、Redis Cluster
  - 不支持读写分离，需要自己实现
  - 文档差（真的很差，几乎没有……）

  

  Redisson：

  

  - 基于Netty实现，采用非阻塞IO，性能高
  - 支持异步请求
  - 支持连接池
  - 支持pipelining、LUA Scripting、Redis Sentinel、Redis Cluster
  - 不支持事务，官方建议以LUA Scripting代替事务
  - 支持在Redis Cluster架构下使用pipelining
  - 支持读写分离，支持读负载均衡，在主从复制和Redis Cluster架构下都可以使用
  - 内建Tomcat Session Manager，为Tomcat 6/7/8提供了会话共享功能
  - 可以与Spring Session集成，实现基于Redis的会话共享
  - 文档较丰富，有中文文档

  

  对于Jedis和Redisson的选择，同样应遵循前述的原理，尽管Jedis比起Redisson有各种各样的不足，但也应该在需要使用Redisson的高级特性时再选用Redisson，避免造成不必要的程序复杂度提升。

  

  **Jedis：**

  
  github：https://github.com/xetorthio/jedis
  文档：https://github.com/xetorthio/jedis/wiki

  

  **Redisson：**

  github：https://github.com/redisson/redisson

  文档：https://github.com/redisson/redisson/wiki

### 消息队列

- 消息队列的使用场景
- 消息的重发补偿解决思路
- 消息的幂等性解决思路（已解答，待补充）
- 消息的堆积解决思路
- 自己如何实现消息队列
- 如何保证消息的有序性

## 框架篇

### Spring

- BeanFactory 和 ApplicationContext 有什么区别
- Spring Bean 的生命周期
- Spring IOC 如何实现
- 说说 Spring AOP
- Spring AOP 实现原理
- 动态代理（cglib 与 JDK）
- Spring 事务实现方式
- Spring 事务底层原理
- 如何自定义注解实现功能
- Spring MVC 运行流程
- Spring MVC 启动流程
- Spring 的单例实现原理
- Spring 框架中用到了哪些设计模式
- Spring 其他产品（Srping Boot、Spring Cloud、Spring Secuirity、Spring Data、Spring AMQP 等）

### Netty

- 为什么选择 Netty
- 说说业务中，Netty 的使用场景
- 原生的 NIO 在 JDK 1.7 版本存在 epoll bug
- 什么是TCP 粘包/拆包
- TCP粘包/拆包的解决办法
- Netty 线程模型
- 说说 Netty 的零拷贝
- Netty 内部执行流程
- Netty 重连实现

## 微服务篇

### 微服务

- 微服务是什么

  ```
  所谓微服务架构，根据微服务架构大神Martin Fowler的描述，就是以业务域或业务功能为边界，将一个大而全的应用拆分为可以独立开发、独立部署、独立测试、独立运行的一组小的应用，并且使用轻量级，通用的机制在这组应用间进行通信。简而言之，微服务就是把一个大型系统分割成多个小而自治的系统，这体现了一种化整为零的思想（分治），实现业务、数据和物理资源的分散化管理。“服务”与传统的“组件”很相似，都是构造软件的“零部件”。以传统软件研发的视角来看，微服务的就是传统组件技术在云端以插件化形式的自然映射。当然，微服务围绕业务分工的粒度更细，整个分布式系统的协作也更为复杂
  ```

- 微服务与SOA

  ```
  传统的基于ESB（企业服务总线）的SOA的尝试，本质上就是要解决企业内部异构系统集成的问题，只是粗粒度的服务和复杂低效的通信方式使得SOA难以大规模应用，而微服务架构采用轻量的API调用服务，经过了互联网公司大规模业务的验证，不存在类似的问题。
  ```

- 微服务框架的作用

  ```
  解决微服务管理、注册发现、服务治理、应用性能监控和链路跟踪等问题
  微服务架构支持更快的响应与上线速度、资源与应用的全面弹性伸缩、应用服务的高可用、细粒度的资源配置等能力，正是企业探索创新业务、应对需求不明确的挑战的必备能力
  重新思考敏捷迭代、DevOps的软件工程
  将应用拆分成多个很小的微服务之后，CIO可以让小团队在几周或者几天内开发、测试和部署一些新特性，并在测试结束后以最快的速度投入生产，加速创业业务孵化，而在传统单体架构下，新版本的发布是不可能这么容易实现的。
  “双模IT”的理念，不少CIO虽然对于这个概念并不敏感，却出于业务发展需要，自然而然地形成了双模IT的部署，稳态面向核心业务，支撑企业业务稳定、可靠、低成本的运行，敏态面向互联网业务需求，解决增量的问题
  ```

- 微服务与外包

  ```
  微服务沉淀IT外包资产
  针对IT外包的三个痛点：迭代缓慢、代码混乱和难以复用，微服务也提供了解决方案。大华股份采用轻舟微服务的持续集成/持续交付（CI/CD）能力，很好地解决了“迭代缓慢”的问题。公司要求外包团队在CI/CD流程上将做好的程序跑起来，一旦跑起来，程序在自动编译后就可以自动部署了。这样，大华股份需要改任何一个东西，都可以在Git上查看情况并进行修改，然后再次启动流程，打出Docker镜像。这种方式很好地解决了工作效率以及成本问题，不需要进行二次开发，只需少许的修改就可以了。
  对于每家外包公司的开发模式都不一样的问题，大华股份通过微服务框架和统一的模板，让外包商都按该模板来写代码，代码结构就可控多了。
  此外，外包商开发的每个服务也同样和文档一起注册到注册中心中，其他的服务开发者，包括大华股份内部团队和其他外包商，如果需要复用这些功能，都可以直接调用这些接口，从而使得不同外包公司的开发成果能够沉淀下来进行复用。
  ```

- [前后端分离是如何做的](https://link.jianshu.com?t=http%3A%2F%2Fblog.720ui.com%2F2016%2Farch_web_server%2F)

- [如何解决跨域](https://link.jianshu.com?t=http%3A%2F%2Fblog.720ui.com%2F2016%2Fweb_cross_domain%2F)

  ```
  josnp, nginx域名路由
  ```

- 微服务哪些框架

  ```
  java  Dubbo 和 Spring Cloud
  ```

- 你怎么理解 RPC 框架

  ```
  因为服务调用方式是 Dubbo 和 Spring Cloud 重要不同点，了解 RPC/gRPC/HTTP/REST 相关概念，有助于对比 Dubbo 和 Spring Cloud。
  
  RPC 是远端过程调用，其调用协议通常包含传输协议和编码协议。
  
  HTTP 严格来说跟 RPC 不是一个层级的概念，HTTP 本身也可以作为 RPC 的传输层协议。
  
  传输协议包含: 如著名的 gRPC 使用的 HTTP 2.0 协议，也有如 Dubbo 一类的自定义报文的 TCP 协议。编码协议包含: 如基于文本编码的 XML Json，也有二进制编码的 ProtoBuf Binpack 等。
  
  所谓的效率优势是针对 HTTP 1.1 协议来讲的，HTTP 2.0 协议已经优化编码效率问题，像 gRPC 这种 RPC 库使用的就是 HTTP 2.0 协议。
  
  在跨语言调用的时候，REST 风格直接把 HTTP 作为应用协议（直接和服务打交道），不同语言之间调用比较方便。
  
  而 RPC 可以把 HTTP 作为一种传输协议（比如 gRPC 使用 HTTP 2.0 协议传输），本身还会封装一层 RPC 框架的应用层协议，不同语言之间调用需要依赖 RPC 协议（需要跨语言 RPC 库实现，比如 Thrift）。
  
  问题：为什么 Dubbo 比 Spring Cloud 性能要高一些？
  
  回答：因为 Dubbo 采用单一长连接和 NIO 异步通讯（保持连接/轮询处理），使用自定义报文的 TCP 协议，并且序列化使用定制 Hessian2 框架，适合于小数据量大并发的服务调用，以及服务消费者机器数远大于服务提供者机器数的情况，但不适用于传输大数据的服务调用。而 Spring Cloud 直接使用 HTTP 协议（但也不是强绑定，也可以使用 RPC 库，或者采用 HTTP 2.0 + 长链接方式（Fegin 可以灵活设置））。
  ```

- 说说 RPC 的实现原理

- 说说 Dubbo 的实现原理

  ```
  Dubbo 是一个分布式服务框架，致力于提供高性能和透明化的 RPC 远程服务调用方案，以及 SOA 服务治理方案。简单的说，Dubbo 就是个服务框架，说白了就是个远程服务调用的分布式框架。
  模块注解：
  
  Provider: 暴露服务的服务提供方。
  Consumer: 调用远程服务的服务消费方。
  Registry: 服务注册与发现的注册中心。
  Monitor: 统计服务的调用次调和调用时间的监控中心。
  Container: 服务运行容器。
  流程详解：
  
  0 服务容器负责启动，加载，运行服务提供者（Standalone 容器）。
  1 服务提供者在启动时，向注册中心注册自己提供的服务（Zookeeper/Redis）。
  2 服务消费者在启动时，向注册中心订阅自己所需的服务。
  3 注册中心返回服务提供者地址列表给消费者，如果有变更，注册中心将基于长连接推送变更数据给消费者。
  4 服务消费者，从提供者地址列表中，基于软负载均衡算法，选一台提供者进行调用，如果调用失败，再选另一台调用。
  5 服务消费者和提供者，在内存中累计调用次数和调用时间，定时每分钟发送一次统计数据到监控中心（根据数据可以动态调整权重）。
  Dubbo 特点
  远程通讯: 提供对多种基于长连接的 NIO 框架抽象封装（非阻塞 I/O 的通信方式，Mina/Netty/Grizzly），包括多种线程模型，序列化（Hessian2/ProtoBuf），以及“请求-响应”模式的信息交换方式。
  集群容错: 提供基于接口方法的透明远程过程调用（RPC），包括多协议支持（自定义 RPC 协议），以及软负载均衡（Random/RoundRobin），失败容错（Failover/Failback），地址路由，动态配置等集群支持。
  自动发现: 基于注册中心目录服务，使服务消费方能动态的查找服务提供方，使地址透明，使服务提供方可以平滑增加或减少机器。
  ```

  

- Spring Cloud

  ```
  Spring Cloud 基于 Spring Boot，为微服务体系开发中的架构问题，提供了一整套的解决方案——服务注册与发现，服务消费，服务保护与熔断，网关，分布式调用追踪，分布式配置管理等。
  Spring Boot 是 Spring 的一套快速配置脚手架，使用默认大于配置的理念，用于快速开发单个微服务。
  
  重点：
  基于 Spring Boot
  云服务、分布式框架集合（众多）
  核心功能：
  分布式/版本化配置
  服务注册和发现
  路由
  服务和服务之间的调用
  负载均衡
  断路器
  分布式消息传递
  ```

- Spring Cloud 工具框架

  ```
  Spring Cloud Config 配置中心，利用 Git 集中管理程序的配置。
  Spring Cloud Netflix 集成众多Netflix的开源软件。
  Spring Cloud Netflix Eureka 服务中心（类似于管家的概念，需要什么直接从这里取，就可以了），一个基于 REST 的服务，用于定位服务，以实现云端中间层服务发现和故障转移。
  Spring Cloud Netflix Hystrix 熔断器，容错管理工具，旨在通过熔断机制控制服务和第三方库的节点，从而对延迟和故障提供更强大的容错能力。
  Spring Cloud Netflix Zuul 网关，是在云平台上提供动态路由，监控，弹性，安全等边缘服务的框架。Web 网站后端所有请求的前门。
  Spring Cloud Netflix Archaius 配置管理 API，包含一系列配置管理API，提供动态类型化属性、线程安全配置操作、轮询框架、回调机制等功能。
  Spring Cloud Netflix Ribbon 负载均衡。
  Spring Cloud Netflix Fegin REST客户端。
  Spring Cloud Bus 消息总线，利用分布式消息将服务和服务实例连接在一起，用于在一个集群中传播状态的变化。
  Spring Cloud for Cloud Foundry 利用 Pivotal Cloudfoundry 集成你的应用程序。
  Spring Cloud Cloud Foundry Service Broker 为建立管理云托管服务的服务代理提供了一个起点。
  Spring Cloud Cluster 集群工具，基于 Zookeeper, Redis, Hazelcast, Consul 实现的领导选举和平民状态模式的抽象和实现。
  Spring Cloud Consul 基于 Hashicorp Consul 实现的服务发现和配置管理。
  Spring Cloud Security 安全控制，在 Zuul 代理中为 OAuth2 REST 客户端和认证头转发提供负载均衡。
  Spring Cloud Sleuth 分布式链路监控，SpringCloud 应用的分布式追踪系统，和 Zipkin，HTrace，ELK 兼容。
  ```

- 你怎么理解 RESTful

  ```
  可以通过 GET、 POST、 PUT、 PATCH、 DELETE 等方式对服务端的资源进行操作。其中：
  
  GET：用于查询资源
  POST：用于创建资源
  PUT：用于更新服务端的资源的全部信息
  PATCH：用于更新服务端的资源的部分信息
  DELETE：用于删除服务端的资源。
  
   /{version}/{resources}/{resource_id}?
   
   状态码	描述
  200	请求成功
  201	创建成功
  400	错误的请求
  401	未验证
  403	被拒绝
  404	无法找到
  409	资源冲突
  500	服务器内部错误
  ```

- [说说如何设计一个良好的 API](https://link.jianshu.com?t=http%3A%2F%2Fblog.720ui.com%2F2017%2Frestful_api%2F)

- [如何理解 RESTful API 的幂等性](https://link.jianshu.com?t=http%3A%2F%2Fblog.720ui.com%2F2016%2Frestful_idempotent%2F)

- 如何保证接口的幂等性

- 说说 CAP 定理、 BASE 理论

  ```
  CAP原则又称CAP定理，指的是在一个分布式系统中， Consistency（一致性）、 Availability（可用性）、Partition tolerance（分区容错性），三者不可得兼。
  
  　　CAP原则是NOSQL数据库的基石。
  
  分布式系统的CAP理论：理论首先把分布式系统中的三个特性进行了如下归纳：
  一致性（C）：在分布式系统中的所有数据备份，在同一时刻是否同样的值。（等同于所有节点访问同一份最新的数据副本）
  可用性（A）：在集群中一部分节点故障后，集群整体是否还能响应客户端的读写请求。（对数据更新具备高可用性）
  分区容忍性（P）：以实际效果而言，分区相当于对通信的时限要求。系统如果不能在时限内达成数据一致性，就意味着发生了分区的情况，必须就当前操作在C和A之间做出选择。
  
  BASE理论
  BASE是Basically Available（基本可用）、Soft state（软状态）和Eventually consistent（最终一致性）三个短语的简写，BASE是对CAP中一致性和可用性权衡的结果，其来源于对大规模互联网系统分布式实践的结论，是基于CAP定理逐步演化而来的，其核心思想是即使无法做到强一致性（Strong consistency），但每个应用都可以根据自身的业务特点，采用适当的方式来使系统达到最终一致性（Eventual consistency）。接下来我们着重对BASE中的三要素进行详细讲解。
  
  1. 基本可用
  基本可用是指分布式系统在出现不可预知故障的时候，允许损失部分可用性——但请注意，这绝不等价于系统不可用，以下两个就是“基本可用”的典型例子。
  
  响应时间上的损失：正常情况下，一个在线搜索引擎需要0.5秒内返回给用户相应的查询结果，但由于出现异常（比如系统部分机房发生断电或断网故障），查询结果的响应时间增加到了1~2秒。
  功能上的损失：正常情况下，在一个电子商务网站上进行购物，消费者几乎能够顺利地完成每一笔订单，但是在一些节日大促购物高峰的时候，由于消费者的购物行为激增，为了保护购物系统的稳定性，部分消费者可能会被引导到一个降级页面。
  2. 弱状态也称为软状态，和硬状态相对，是指允许系统中的数据存在中间状态，并认为该中间状态的存在不会影响系统的整体可用性，即允许系统在不同节点的数据副本之间进行数据听不的过程存在延时
  3. 最终一致性:
     因果一致性： 因果一致性是指，如果进程A在更新完某个数据项后通知了进程B，那么进程B之后对该数据项的访问都应该能够获取到进程A更新后的最新值，并且如果进程B要对该数据项进行更新操作的话，务必基于进程A更新后的最新值，即不能发生丢失更新情况。与此同时，与进程A无因果关系的进程C的数据访问则没有这样的限制。
  
  	读己之所写：  读己之所写是指，进程A更新一个数据项之后，它自己总是能够访问到更新过的最新值，而不会看到旧值。也就是说，对于单个数据获取者而言，其读取到的数据一定不会比自己上次写入的值旧。因此，读己之所写也可以看作是一种特殊的因果一致性。
  
  	会话一致性： 会话一致性将对系统数据的访问过程框定在了一个会话当中：系统能保证在同一个有效的会话中实现“读己之所写”的一致性，也就是说，执行更新操作之后，客户端能够在同一个会话中始终读取到该数据项的最新值。
  
  	单调读一致性： 单调读一致性是指如果一个进程从系统中读取出一个数据项的某个值后，那么系统对于该进程后续的任何数据访问都不应该返回更旧的值。
  
  	单调写一致性： 单调写一致性是指，一个系统需要能够保证来自同一个进程的写操作被顺序地执行。
  ```

- 怎么考虑数据一致性问题

  ```
  # Saga 是一个长活事务，可被分解成可以交错运行的子事务集合。其中每个子事务都是一个保持数据库一致性的真实事务。Saga 中的事务相互关联，应作为（非原子）单位执行。任何未完全执行的 Saga 是不满足要求的，如果发生，必须得到补偿。要修正未完全执行的部分，每个 saga 子交易 T1 应提供对应补偿事务 C1。
    恢复机制：向后恢复 补偿所有已完成的事务，如果任一子事务失败向前恢复 重试失败的事务，假设每个子事务最终都会成功
  
  # 两阶段提交 Two-Phase Commit (2PC):两阶段提交协议是一种分布式算法，用于协调参与分布式原子事务的所有进程，以保证他们均完成提交或中止（回滚）事务。1. 投票阶段 协调器向所有服务发起投票请求，服务回答 yes 或 no。如果有任何服务回复 no 以拒绝或超时，协调器则在下一阶段发送中止消息。 2. 决定阶段 如果所有服务都回复 yes，协调器则向服务发送 commit 消息，接着服务告知事务完成或失败。如果任何服务提交失败， 协调器将启动额外的步骤以中止该事务。
  # Try-Confirm/Cancel (TCC) TCC 也是补偿型事务模式，支持两阶段的商业模型。
  1. 尝试阶段 将服务置于待处理状态。例如，收到尝试请求时，航班预订服务将为客户预留一个座位，并在数据库插入客户预订记录，将记录设为预留状态。如果任何服务失败或超时，协调器将在下一阶段发送取消请求。
  2. 确认阶段 将服务设为确认状态。确认请求将确认客户预订的座位，这时服务已可向客户收取机票费用。数据库中的客户预订记录也会被更新为确认状态。如果任何服务无法确认或超时，协调器将重试确认请求直到成功，或在重试了一定次数后采取回退措施，比如人工干预。
  与 saga 相比，TCC 的优势在于，尝试阶段将服务转为待处理状态而不是最终状态，这使得设计相应的取消操作轻而易举。TCC 的缺点是其两阶段协议需要设计额外的服务待处理状态，以及额外的接口来处理尝试请求。另外，TCC 处理事务请求所花费的时间可能是 saga 的两倍，因为 TCC 需要与每个服务进行两次通信，并且其确认阶段只能在收到所有服务对尝试请求的响应后开始。
  事件驱动的架构
  和 TCC 一样，在事件驱动的架构中，长活事务涉及的每个服务都需要支持额外的待处理状态。接收到事务请求的服务会在其数据库中插入一条新的记录，将该记录状态设为待处理并发送一个新的事件给事务序列中的下一个服务。
  因为在插入记录后服务可能崩溃，我们无法确定是否新事件已发送，所以每个服务还需要额外的事件表来跟踪当前长活事务处于哪一步。
  一旦长活事务中的最后一个服务完成其子事务，它将通知它在事务中的前一个服务。接收到完成事件的服务将其在数据库中的记录状态设为完成。
  ```

- 说说最终一致性的实现方案

- [你怎么看待微服务](https://link.jianshu.com?t=http%3A%2F%2Fblog.720ui.com%2F2017%2Fmsa_intro%2F)

- [微服务与 SOA 的区别](https://link.jianshu.com?t=http%3A%2F%2Fblog.720ui.com%2F2017%2Fmsa_soa%2F)

  ```
  方面	SOA	微服务架构
  应用粒度	多个系统整合成一个服务，粒度大	一个系统拆分成多个服务，粒度小
  服务架构	企业服务总线（ESB），集中式架构	服务自治，松散式架构
  服务规模	服务规模较小	服务规模膨胀
  服务部署	单体架构，业务耦合	功能独立，独立部署
  ```

- [如何拆分服务](https://link.jianshu.com?t=http%3A%2F%2Fblog.720ui.com%2F2017%2Fmsa_design%2F)

- [微服务如何进行数据库管理](https://link.jianshu.com?t=http%3A%2F%2Fblog.720ui.com%2F2017%2Fmsa_design%2F)

- [如何应对微服务的链式调用异常](https://link.jianshu.com?t=http%3A%2F%2Fblog.720ui.com%2F2017%2Fmsa_design%2F)

- [对于快速追踪与定位问题](https://link.jianshu.com?t=http%3A%2F%2Fblog.720ui.com%2F2017%2Fmsa_design%2F)

- [微服务的安全](https://link.jianshu.com?t=http%3A%2F%2Fblog.720ui.com%2F2017%2Fmsa_design%2F)

- 微服务CI/CD

  ```
  gitlab + jenkins + docker + k8s
  在开发机开发代码后提交到gitlab
  之后通过webhook插件触发jenkins进行构建，jenkins将代码打成docker镜像，push到docker-registry
  之后将在k8s-master上执行rc、service的创建，进而创建Pod，从私服拉取镜像，根据该镜像启动容器
  
  1. 安装gitlab
  2. 安装jenkins
  3. 使用webhooks来实现当git客户端push代码到gitlab后，jenkins会立即去gitlab拉取代码并构建。
  4. 完成jenkins自动构建之后，自动的将jar包部署到应用服务器并启动服务。
  5. docker-registry
  
  代码检查工具
  代码分析工具：SonarQube：重复代码， 潜在bug， 代码风格问题，缺乏单元测试
  制品/包管理工具：Nexus
  自动化测试框架： JUnit、 PHP Unit、Python Unit Test、JMeter
  已支持的代码管理工具：Ansible
  ```

  分布式

  

  #### influxdb

  1、数据格式

  在 InfluxDB 中，我们可以粗略的将要存入的一条数据看作**一个虚拟的 key 和其对应的 value(field value)**。格式如下：

  ```
  `cpu_usage,host``=``server01,region``=``us``-``west value``=``0.64` `1434055562000000000`
  ```

  虚拟的 key 包括以下几个部分： database, retention policy, measurement, tag sets, field name, timestamp。

  - database: 数据库名，在 InfluxDB 中可以创建多个数据库，不同数据库中的数据文件是隔离存放的，存放在磁盘上的不同目录。
  - retention policy: 存储策略，用于设置数据保留的时间，每个数据库刚开始会自动创建一个默认的存储策略 autogen，数据保留时间为永久，之后用户可以自己设置，例如保留最近2小时的数据。插入和查询数据时如果不指定存储策略，则使用默认存储策略，且默认存储策略可以修改。InfluxDB 会定期清除过期的数据。
  - measurement: 测量指标名，例如 cpu_usage 表示 cpu 的使用率。
  - tag sets: tags 在 InfluxDB 中会按照字典序排序，不管是 tagk 还是 tagv，只要不一致就分别属于两个 key，例如 host=server01,region=us-west 和 host=server02,region=us-west 就是两个不同的 tag set。
  - tag--标签，在InfluxDB中，tag是一个非常重要的部分，表名+tag一起作为数据库的索引，是“key-value”的形式。
  - field name: 例如上面数据中的 value 就是 fieldName，InfluxDB 中支持一条数据中插入多个 fieldName，这其实是一个语法上的优化，在实际的底层存储中，是当作多条数据来存储。
  - timestamp: 每一条数据都需要指定一个时间戳，在 TSM 存储引擎中会特殊对待，以为了优化后续的查询操作。

  2、与传统数据库中的名词做比较

  | influxDB中的名词 | 传统数据库中的概念 |
  | ---------------- | ------------------ |
  | database         | 数据库             |
  | measurement      | 数据库中的表       |
  | points           | 表里面的一行数据   |

  3、Point

  Point由时间戳（time）、数据（field）、标签（tags）组成。

  Point相当于传统数据库里的一行数据，如下表所示：

   

  | Point属性 | 传统数据库中的概念                               |
  | --------- | ------------------------------------------------ |
  | time      | 每个数据记录时间，是数据库中的主索引(会自动生成) |
  | fields    | 各种记录值（没有索引的属性）                     |
  | tags      | 各种有索引的属性                                 |

  4、Series

  ​       Series 相当于是 InfluxDB 中一些数据的集合，在同一个 database 中，retention policy、measurement、tag sets 完全相同的数据同属于一个 series，同一个 series 的数据在物理上会按照时间顺序排列存储在一起。

  5、Shard

  ​       Shard 在 InfluxDB 中是一个比较重要的概念，它和 retention policy 相关联。每一个存储策略下会存在许多 shard，每一个 shard 存储一个指定时间段内的数据，并且不重复，例如 7点-8点 的数据落入 shard0 中，8点-9点的数据则落入 shard1 中。每一个 shard 都对应一个底层的 tsm 存储引擎，有独立的 cache、wal、tsm file。

  6、组件

  TSM 存储引擎主要由几个部分组成： cache、wal、tsm file、compactor。

  1）Cache：cache 相当于是 LSM Tree 中的 memtabl。插入数据时，实际上是同时往 cache 与 wal 中写入数据，可以认为 cache 是 wal 文件中的数据在内存中的缓存。当 InfluxDB 启动时，会遍历所有的 wal 文件，重新构造 cache，这样即使系统出现故障，也不会导致数据的丢失。

  cache 中的数据并不是无限增长的，有一个 maxSize 参数用于控制当 cache 中的数据占用多少内存后就会将数据写入 tsm 文件。如果不配置的话，默认上限为 25MB，每当 cache 中的数据达到阀值后，会将当前的 cache 进行一次快照，之后清空当前 cache 中的内容，再创建一个新的 wal 文件用于写入，剩下的 wal 文件最后会被删除，快照中的数据会经过排序写入一个新的 tsm 文件中。

  2）WAL：wal 文件的内容与内存中的 cache 相同，其作用就是为了持久化数据，当系统崩溃后可以通过 wal 文件恢复还没有写入到 tsm 文件中的数据。

  3）TSM File：单个 tsm file 大小最大为 2GB，用于存放数据。

  4）Compactor：compactor 组件在后台持续运行，每隔 1 秒会检查一次是否有需要压缩合并的数据。

  主要进行两种操作，一种是 cache 中的数据大小达到阀值后，进行快照，之后转存到一个新的 tsm 文件中。

  另外一种就是合并当前的 tsm 文件，将多个小的 tsm 文件合并成一个，使每一个文件尽量达到单个文件的最大大小，减少文件的数量，并且一些数据的删除操作也是在这个时候完成。

  7、目录与文件结构

  InfluxDB 的数据存储主要有三个目录。默认情况下是 meta, wal 以及 data 三个目录。

  meta 用于存储数据库的一些元数据，meta 目录下有一个 `meta.db` 文件。

  wal 目录存放预写日志文件，以 `.wal` 结尾。

  data 目录存放实际存储的数据文件，以 `.tsm` 结尾。

  上面几张图中，_internal为数据库名，monitor为存储策略名称，再下一层目录中的以数字命名的目录是 shard 的 ID 值。

  存储策略下有两个 shard，ID 分别为 1 和 2，shard 存储了某一个时间段范围内的数据。再下一级的目录则为具体的文件，分别是 `.wal` 和 `.tsm` 结尾的文件。

  8. 压缩算法

     nfluxdb根据不同的数据类型会采用不同的压缩算法。

     - int

     　　首先使用ZigZag算法进行编码，如果编码后的值小于 (1 << 60 ) - 1，使用simple8b算法；

     　　如果大于该值，不压缩；

     - timestamp

     　　时间戳为独立的数据类型，并且具有一定的规律可循，在InfluxDB中， 针对时间戳先执行排序操作后使用差分编码算法进行编码，然后再根据编码结果采用不同的算法。　　

     　　解释如下：

     　　1、根据输入的原始数组arrValues计算出差值数组deltaValues；

     　　2、如果差值数组的所有值相同，使用RLE编码算法；

     　　3、如果差值数组的所有值不同，并且差值数组的最大值大于（1 << 60）- 1，使用Raw编码算法；

     　　4、如果差值数组的所有值不同，并且差值数组的最大值不大于（1 << 60）- 1，使用Packed编码；

     - float

     　　使用 Facebook Gorilla paper提供的浮点数压缩算法

     - bool

     　　只有1位数据，采用简单的位数据打包策略

     - string

     　　采用snappy算法

  ### Netty

  #### 1.Netty 是什么？ 

  Netty 是一款基于 NIO（Nonblocking I/O，非阻塞IO）开发的网络通信框架，对比于 BIO（Blocking I/O，阻塞IO），他的并发性能得到了很大提高。难能可贵的是，在保证快速和易用性的同时，并没有丧失可维护性和性能等优势。

  #### 2.Netty 的特点是什么？

  高并发：Netty 是一款基于 NIO（Nonblocking IO，非阻塞IO）开发的网络通信框架，对比于 BIO（Blocking I/O，阻塞IO），他的并发性能得到了很大提高。

  传输快：Netty 的传输依赖于零拷贝特性，尽量减少不必要的内存拷贝，实现了更高效率的传输。

  封装好：Netty 封装了 NIO 操作的很多细节，提供了易于使用调用接口。

  #### 3.什么是 Netty 的零拷贝？

  Netty 的零拷贝主要包含三个方面：

  Netty 的接收和发送 ByteBuffer 采用 DIRECT BUFFERS，使用堆外直接内存进行 Socket 读写，不需要进行字节缓冲区的二次拷贝。如果使用传统的堆内存（HEAP BUFFERS）进行 Socket 读写，JVM 会将堆内存 Buffer 拷贝一份到直接内存中，然后才写入 Socket 中。相比于堆外直接内存，消息在发送过程中多了一次缓冲区的内存拷贝。

  Netty 提供了组合 Buffer 对象，可以聚合多个 ByteBuffer 对象，用户可以像操作一个 Buffer 那样方便的对组合 Buffer 进行操作，避免了传统通过内存拷贝的方式将几个小 Buffer 合并成一个大的 Buffer。

  Netty 的文件传输采用了 transferTo 方法，它可以直接将文件缓冲区的数据发送到目标 Channel，避免了传统通过循环 write 方式导致的内存拷贝问题。

  #### 4.Netty 的优势有哪些？

  使用简单：封装了 NIO 的很多细节，使用更简单。

  功能强大：预置了多种编解码功能，支持多种主流协议。

  定制能力强：可以通过 ChannelHandler 对通信框架进行灵活地扩展。

  性能高：通过与其他业界主流的 NIO 框架对比，Netty 的综合性能最优。

  稳定：Netty 修复了已经发现的所有 NIO 的 bug，让开发人员可以专注于业务本身。

  社区活跃：Netty 是活跃的开源项目，版本迭代周期短，bug 修复速度快。

  #### 5.Netty 的应用场景有哪些？

  典型的应用有：阿里分布式服务框架 Dubbo，默认使用 Netty 作为基础通信组件，还有 RocketMQ 也是使用 Netty 作为通讯的基础。

  #### 6.Netty 高性能表现在哪些方面？

  IO 线程模型：同步非阻塞，用最少的资源做更多的事。

  内存零拷贝：尽量减少不必要的内存拷贝，实现了更高效率的传输。

  内存池设计：申请的内存可以重用，主要指直接内存。内部实现是用一颗二叉查找树管理内存分配情况。

  串形化处理读写：避免使用锁带来的性能开销。

  高性能序列化协议：支持 protobuf 等高性能序列化协议。

  #### 7.Netty 和 Tomcat 的区别？

  作用不同：Tomcat 是 Servlet 容器，可以视为 Web 服务器，而 Netty 是异步事件驱动的网络应用程序框架和工具用于简化网络编程，例如TCP和UDP套接字服务器。

  协议不同：Tomcat 是基于 http 协议的 Web 服务器，而 Netty 能通过编程自定义各种协议，因为 Netty 本身自己能编码/解码字节流，所有 Netty 可以实现，HTTP 服务器、FTP 服务器、UDP 服务器、RPC 服务器、WebSocket 服务器、[Redis](https://cloud.tencent.com/product/crs?from=10680) 的 Proxy 服务器、[MySQL](https://cloud.tencent.com/product/cdb?from=10680) 的 Proxy 服务器等等。

  #### 8.Netty 中有那种重要组件？

  Channel：Netty 网络操作抽象类，它除了包括基本的 I/O 操作，如 bind、connect、read、write 等。

  EventLoop：主要是配合 Channel 处理 I/O 操作，用来处理连接的生命周期中所发生的事情。

  ChannelFuture：Netty 框架中所有的 I/O 操作都为异步的，因此我们需要 ChannelFuture 的 addListener()注册一个 ChannelFutureListener 监听事件，当操作执行成功或者失败时，监听就会自动触发返回结果。

  ChannelHandler：充当了所有处理入站和出站数据的逻辑容器。ChannelHandler 主要用来处理各种事件，这里的事件很广泛，比如可以是连接、数据接收、异常、数据转换等。

  ChannelPipeline：为 ChannelHandler 链提供了容器，当 channel 创建时，就会被自动分配到它专属的 ChannelPipeline，这个关联是永久性的。

  #### 9.Netty 发送消息有几种方式？

  Netty 有两种发送消息的方式：

  直接写入 Channel 中，消息从 ChannelPipeline 当中尾部开始移动；

  写入和 ChannelHandler 绑定的 ChannelHandlerContext 中，消息从 ChannelPipeline 中的下一个 ChannelHandler 中移动。

  #### 10.默认情况 Netty 起多少线程？何时启动？

  Netty 默认是 CPU 处理器数的两倍，bind 完之后启动。

  #### 11.Netty 支持哪些心跳类型设置？

  readerIdleTime：为读超时时间（即测试端一定时间内未接受到被测试端消息）。

  writerIdleTime：为写超时时间（即测试端一定时间内向被测试端发送消息）。

  allIdleTime：所有类型的超时时间。

### 虚拟化



VPS（虚拟专用服务器）的虚拟技术有很多种，VPS就是通过某种虚拟技术把一台服务器分成多个虚拟服务器。VPS常用的虚拟技术有OpenVZ、Xen、KVM三种，不同的虚拟机的VPS相同的配置可能价格相差很大，那么这三种虚拟技术到底是什么，它们之间又有什么区别？本文对OpenVZ、Xen、KVM三种虚拟技术做一个简单的介绍，并比较它们之间的差异，希望对以后你们选择VPS有点帮助。



##### **OpenVZ虚拟技术**

OpenVZ的介绍：OpenVZ是操作系统级别的虚拟技术，即运行在Linux上，并在底层操作系统上运行一层应用，通过虚拟化技术将一个服务器安装成多个操作系统的实例，这样每个实例就是一个VPS，这意味着易于理解和低权重开销，并且应用无需近过虚拟指令可以直接运行在CPU上，因此一般OpenVZ会有更好的性能，并且相比于其他两种常见的虚拟技术，价格低廉。

OpenVZ的优点：

1. OpenVZ价格低，相同价格可以买到更高的配置，内存与CPU普遍较好。
2. 共用一个内核，效率高，性能较好。

OpenVZ的缺点：

1. OpenVZ只能安装Linux，不能安装Windows。
2. 共用母核，每个VPS实例不能单独修改内核（因此按照常规操作无法开启bbr）。
3. 超卖！！！！基本没有不超卖的OpvenVZ。因为共用一个母机的CPU和内存，超卖现象严重会导致速度降低，CPU和内存往往也没有VPS服务商保证的那么好。

##### **Xen虚拟技术**

Xen的介绍：Xen是半虚拟化技术，它并不是一个真正的虚拟机，而是相当于自己运行一个内核的实例，可以自由加载内核模块、虚拟的内存和IO。Xen虚拟技术可以分为两种，Xen PV和Xen HVM，其中，Xen PV只支持Linux系统，而Xen HVM支持WIndows系统，性能则是前者高于后者。

Xen的优点：

1. 独占内存，虽然小但是保证能够分配得到。
2. 半虚拟化保证了相比于OpenVZ超卖现象不会很严重，超卖对性能的影响也没有OpenVZ那么大。

Xen的缺点：

1. 相同价位，对比与OpenVZ，内存更小，CPU、IO性能更差。

##### **KVM虚拟技术**

KVM的介绍：KVM是完全虚拟的，各个VPS实例之间不共用母机的内核，各自之间都是相互独立的。并且只要你的配置足够，KVM理论上支持Linux和Windows上的任何版本。

KVM的优点：

1. 完全虚拟化，可以装Linux或者Winodws。
2. 独用内核、内存、CPU，完美支持TCP BBR加速。

KVM的缺点：

1. 因为KVM支持任何操作系统，如果同一个node的装了过多的windows，有可能会影响极其硬盘的使用。

##### **OpenVZ、Xen、KVM三种虚拟技术之间的比较**

综上所述，

1. OpenVZ在不超售的情况下是性价比最高的一种虚拟化技术：价格低，性能好。但是！！！基本没有一个VPS服务商不超售OpenVZ，所以往往拿到的机子都是与描述的相比缩水很多的，人越多越卡，因此不建议使用。
2. Xen这个虚拟化技术说实话我没有用过，不过它有PV和HVM两种，对于系统的支持时分开的，相对来说稳定性更好一些。
3. KVM是我推荐的一个虚拟化技术，独占内核、内存，相比于OpenVZ来说，稳定性更好，受超售的影响小，其实也不会有那么多人在配置那么低的VPS上硬要装Winodws的，而且它完美支持BBR加速。



##### IAAS

作为 IaaS 层的云操作系统，OpenStack 为虚拟机提供并管理三大类资源：计算、网络和存储。



##### OpenStack 与kvm

```
Openstack是云平台一整天相互独立管理工具的集合，从stack这个单词的本身定义就能大概理解。云计算是计算机、虚拟化计算、网络通信、分布式计算、分布式存储等多重计算融合的一种计算，严格意义上，本人更倾向把Cloud Computing理解为一种全新的使用资源（服务器、网络、存储介质）的思路或方法。通过云计算，将海量的服务器、网络、存储等组织成一个大的资源池，用户可以通过前端随时随地申请可以量化的计算资源、网络资源、存储资源，这种按需划分资源的模式，可以大大提高资源的使用率，并且用户不用关心物理资源存放在哪，也不用自己运维。

这其中一项关键的技术就是虚拟化技术，虚拟化技术运行在底层硬件和OS之间，对上层OS或APPs屏蔽底层硬件的物理属性，那么KVM就是这种虚拟化技术之一，Openstack是一个开源项目，除了KVM当然也兼任其它的虚拟化技术比如Xen、Hyper-V、VMware.
```

KVM(Kernel-based Virtual Machine)基于内核的虚拟机

```
KVM是集成到Linux内核的Hypervisor，是X86架构且硬件支持虚拟化技术（Intel VT或AMD-V）的Linux的全虚拟化解决方案。它是Linux的一个很小的模块，利用Linux做大量的事，如任务调度、内存管理与硬件设备交互等。
KVM最大的好处就在于它是与Linux内核集成的，所以速度很快。
```

##### VMWare (Virtual Machine ware)

```
VMWare (Virtual Machine ware)是一个“虚拟PC”虚拟机管理管理软件。它的产品可以使你在一台机器上同时运行二个或更多Windows、DOS、LINUX系统。与“多启动”系统相比，VMWare采用了完全不同的概念。多启动系统在一个时刻只能运行一个系统，在系统切换时需要重新启动机器。VMWare是真正“同时”运行，多个操作系统在主系统的平台上，就象标准Windows应用程序那样切换。而且每个操作系统你都可以进行虚拟的分区、配置而不影响真实硬盘的数据，你甚至可以通过网卡将几台虚拟机用网卡连接为一个局域网，极其方便。安装在VMware操作系统性能上比直接安装在硬盘上的系统低不少，因此，比较适合学习和测试。
```



### 分布式

- 谈谈业务中使用分布式的场景
- Session 分布式方案
- 分布式锁的场景
- 分布是锁的实现方案
- 分布式事务
- 集群与负载均衡的算法与实现
- [说说分库与分表设计](https://link.jianshu.com?t=http%3A%2F%2Fblog.720ui.com%2F2017%2Fmysql_core_08_multi_db_table%2F)
- [分库与分表带来的分布式困境与应对之策](https://link.jianshu.com?t=http%3A%2F%2Fblog.720ui.com%2F2017%2Fmysql_core_09_multi_db_table2%2F)

### 安全问题

- [安全要素与 STRIDE 威胁](https://link.jianshu.com?t=http%3A%2F%2Fblog.720ui.com%2F2017%2Fsecurity_stride%2F)

- [防范常见的 Web 攻击](https://link.jianshu.com?t=http%3A%2F%2Fblog.720ui.com%2F2016%2Fsecurity_web%2F)

  ```
  # SQL注入攻击
  使用预编译的PrepareStatement是必须的，但是一般我们会从两个方面同时入手。
  Web端
  有效性检验。
  限制字符串输入的长度。
  服务端
  不用拼接SQL字符串。
  使用预编译的PrepareStatement。
  有效性检验。(为什么服务端还要做有效性检验？第一准则，外部都是不可信的，防止攻击者绕过Web端请求)
  过滤SQL需要的参数中的特殊字符。比如单引号、双引号。
  # XSS攻击
  用户输入一个可执行脚本
  如何防范XSS攻击
  前端，服务端，同时需要字符串输入的长度限制。
  前端，服务端，同时需要对HTML转义处理。将其中的”<”,”>”等特殊字符进行转义编码。
  # CSRF攻击
  跨站点请求伪造，指攻击者通过跨站请求，以合法的用户的身份进行非法操作。可以这么理解CSRF攻击：攻击者盗用你的身份，以你的名义向第三方网站发送恶意请求。CRSF能做的事情包括利用你的身份发邮件，发短信，进行交易转账，甚至盗取账号信息。
  如何防范CSRF攻击
  安全框架，例如Spring Security。
  token机制。在HTTP请求中进行token验证，如果请求中没有token或者token内容不正确，则认为CSRF攻击而拒绝该请求。
  验证码。通常情况下，验证码能够很好的遏制CSRF攻击，但是很多情况下，出于用户体验考虑，验证码只能作为一种辅助手段，而不是最主要的解决方案。
  referer识别。在HTTP Header中有一个字段Referer，它记录了HTTP请求的来源地址。如果Referer是其他网站，就有可能是CSRF攻击，则拒绝该请求。但是，服务器并非都能取到Referer。很多用户出于隐私保护的考虑，限制了Referer的发送。在某些情况下，浏览器也不会发送Referer，例如HTTPS跳转到HTTP。
  # 文件上传漏洞
  文件上传漏洞，指的是用户上传一个可执行的脚本文件，并通过此脚本文件获得了执行服务端命令的能力。
  如何防范文件上传漏洞
  1. 文件上传的目录设置为不可执行。
  2. 判断文件类型。在判断文件类型的时候，可以结合使用MIME Type，后缀检查等方式。因为对于上传文件，不能简单地通过后缀名称来判断文件的类型，因为攻击者可以将可执行文件的后缀名称改为图片或其他后缀类型，诱导用户执行。
  3. 对上传的文件类型进行白名单校验，只允许上传可靠类型。
  4. 上传的文件需要进行重新命名，使攻击者无法猜想上传文件的访问路径，将极大地增加攻击成本，同时向shell.php.rar.ara这种文件，因为重命名而无法成功实施攻击。
  5. 限制上传文件的大小。
  6. 单独设置文件服务器的域名
  # 访问控制
  一般来说，“基于URL的访问控制”是最常见的。
  1. 垂直权限管理
  访问控制实际上是建立用户与权限之间的对应关系，即“基于角色的访问控制”，RBAC。不同角色的权限有高低之分。高权限角色访问低权限角色的资源往往是被允许的，而低权限角色访问高权限的资源往往被禁止的。在配置权限时，应当使用“最小权限原则”，并使用“默认拒绝”的策略，只对有需要的主体单独配置”允许”的策略，这在很多时候能够避免发生“越权访问”。
  例如，Spring Security， Apache Shiro都可以建立垂直权限管理。
  2. 水平权限管理
  水平权限问题在同一个角色上，系统只验证了访问数据的角色，没有对角色内的用户做细分，由于水平权限管理是系统缺乏一个数据级的访问控制所造成的，因此水平权限管理又可以称之为“基于数据的访问控制”。
  举个理解，比如我们之前的一个助手产品，客户端用户删除评论功能，如果没有做水平权限管理，即设置只有本人才可以删除自己的评论，那么用户通过修改评论id就可以删除别人的评论这个就存在危险的越权操作。
  这个层面，基本需要我们业务层面去处理，但是这个也是最为经常遗落的安全点。
  ```

  

- [服务端通信安全攻防](https://link.jianshu.com?t=http%3A%2F%2Fblog.720ui.com%2F2016%2Fsecurity_data_transmission%2F)

- [HTTPS 原理剖析](https://link.jianshu.com?t=http%3A%2F%2Fblog.720ui.com%2F2016%2Fsecurity_https%2F)

- [HTTPS 降级攻击](https://link.jianshu.com?t=http%3A%2F%2Fblog.720ui.com%2F2016%2Fsecurity_https_tls%2F)

- [授权与认证](https://link.jianshu.com?t=http%3A%2F%2Fblog.720ui.com%2F2017%2Fmsa_oauth2%2F)

- [基于角色的访问控制](https://link.jianshu.com?t=http%3A%2F%2Fblog.720ui.com%2F2017%2Fmsa_rbac%2F)

- [基于数据的访问控制](https://link.jianshu.com?t=http%3A%2F%2Fblog.720ui.com%2F2017%2Fmsa_rbac_data%2F)

- web防火墙

  ```
  系统通过防火墙WAF防御SQL注入、XSS跨站脚本、常见Web服务器插件漏洞、木马上传、非授权核心资源访问等OWASP常见攻击，过滤海量恶意攻击，避免您的网站资产数据泄露，保障网站的安全与可用性
  深信服
  华为
  ```

- 加固

  ```
  1.	网络设备加固内容
  网络设备安全加固包含但不限于以下内容：
  (1)	OS升级
  (2)	帐号和口令管理
  (3)	认证和授权策略调整
  (4)	网络与服务加固
  (5)	访问控制策略增强
  (6)	通讯协议、路由协议加固
  (7)	日志审核策略增强
  (8)	加密管理加固
  (9)	设备其他安全配置增强
  2.	 主机操作系统加固内容
  主机操作系统安全加固包含但不限于以下内容：
  (1)	系统漏洞补丁管理
  (2)	帐号和口令管理
  (3)	认证、授权策略调整
  (4)	网络与服务、进程和启动加固
  (5)	文件系统权限增强
  (6)	访问控制管理
  (7)	通讯协议加固
  (8)	日志审核功能增强
  (9)	防DDOS攻击增强
  (10)	其他安全配置增强
  3.	 数据库加固内容
  数据库安全加固包含但不限于以下内容：
  (1)	漏洞补丁管理
  (2)	帐号和口令管理
  (3)	认证、授权策略调整
  (4)	访问控制管理
  (5)	通讯协议加固
  (6)	日志审核功能增强
  (7)	其他安全配置增强
  4.	 中间件及常见网络服务加固内容
  中间件及常见网络服务安全加固包含但不限于以下内容：
  (1)	漏洞补丁管理
  (2)	帐号和口令管理
  (3)	认证、授权策略调整
  (4)	通讯协议加固
  (5)	日志审核功能增强
  (6)	其他安全配置增强
  
  工具：  护卫神
  ```

  ### 电力系统

  https://blog.csdn.net/god881205/article/details/50715037

### 设计方法论

- 六边形理论

  ```
  六边形架构的意图
  采用同等的方式，应用可以通过用户，程序，自动化测试或批处理脚本来驱动，而独立于最终的运行环境及数据库进行开发和测试。
  
  当外部事件到达端口的时候，相应的适配器将其转化成合适的过程调用或者消息，然后传递给应用，而应用对输入设备一无所知。输出内容时，应用通过端口把要传递出去的消息传给适配器，适配器再针对信息接收者的具体实现要求将其转化成合适的信号。从语义上来说，应用跟它周围的适配器有着良好的互动，而对适配器外部的一切无感知。
  
  这是一种设计模式，被Cockburn定义为“端口和适配器模式“，设计模式不仅指导了代码的实现，同时支持结构的实现，又是一种解耦合的技巧。
  
  所需解决的问题场景
  不能解决问题的架构，都只是架构师手中的玩具。六边形架构面对的一个典型问题是业务逻辑与用户界面的代码交叉，这是开发中一个非常令人头痛的问题，有三个恶果：
  
  系统无法方便地进行自动化测试，因为部分逻辑依赖界面元素的，比如输入框的长度或按钮的位置，而这些细节又是易变的；
  同样，无法把一个面向人机交互的系统移植到一个自动化处理的系统
  另外，应用程序之间的相互驱动变得很困难，有时甚至不可能的
  “万能的那一层”出现了，可以在架构里增加一个新的层，并承诺不会有业务逻辑被放到着一新层里。然而随着时间的推移，会发现新的层里还是掺杂了业务逻辑，于是老问题又出现了。
  
  怎么办呢？假设一下，如果应用提供的每一个功能都有相应的API会是怎样的结果呢？QA可以通过自动化测试脚本来监测新改的代码，检验是否会破坏已有的功能。业务专家在GUI出来之前就可以创建自动化测试用例，作为程序员们检测是否正确完成工作的依据，同时，这也将成为测试部门所运行的测试的一部分。应用以"headless"模式部署，其它程序通过调用API的方式使用所提供的功能。这种方式使得复杂系统的设计变得容易，面向业务的应用之间不需要人工干预就可以互相调用。最后，回归测试检测到出现问题的地方，并加以修复，而保证业务逻辑不会进入表现层。
  
  另一个典型的问题是，如果应用绑定了外部数据库或其它服务，当数据库宕机或者正在迁移的时候，依赖数据库的程序就无法正常工作。这会导致响应延迟，这是一种相当糟糕的体验。
  
  这两个问题之间没有明显的联系，但它们之间看起来是对称的。这又是一种面向接口的设计么？ 可以这样理解，因为接口的概念外延太大了，而在具体的编程语言实现中，interface 有往往太小了。这里把它明确为端口和适配器。
  ```

- 领域驱动设计

- [DCI架构]

  ```
  DCI代表Data, Context, Interaction。
  ```

  

### 网络

- 五层模型与7层模型

  ```
  物理层，链路层、网络层、传输层、应用层
  物理层，链路层、网络层、传输层、表示层、会话层、应用层
  物理层： 
  链路层： 网桥，网卡，以太交换机  iee802.3 ARP 
  网络层： 路由器，三层交换机 ip icmp igmp
  传输层： 四层路由器，四层交换机 tcp udp
  应用层： http，ftp，smtp，dns
  ```

- 对等网络

- DNS解析

  ```
  1. 现在我有一台计算机，通过ISP接入了互联网，那么ISP就会给我分配一个DNS服务器，这个DNS服务器不是权威服务器，而是相当于一个代理的dns解析服务器，他会帮你迭代权威服务器返回的应答，然后把最终查到IP返回给你。
  
  2.现在的我计算机要向这台ISPDNS发起请求查询www.baidu.com这个域名了，(经网友提醒：这里其实准确来说不是ISPDNS，而应该是用户自己电脑网络设置里的DNS，并不一定是ISPDNS。比如也有可能你手工设置了8.8.8.8)
  
  3.ISPDNS拿到请求后，先检查一下自己的缓存中有没有这个地址，有的话就直接返回。这个时候拿到的ip地址，会被标记为非权威服务器的应答。
  
  4.如果缓存中没有的话，ISPDNS会从配置文件里面读取13个根域名服务器的地址（这些地址是不变的，直接在BIND的配置文件中），
  
  5.然后像其中一台发起请求。
  
  6.根服务器拿到这个请求后，知道他是com.这个顶级域名下的，所以就会返回com域中的NS记录，一般来说是13台主机名和IP。
  
  7.然后ISPDNS向其中一台再次发起请求，com域的服务器发现你这请求是baidu.com这个域的，我一查发现了这个域的NS，那我就返回给你，你再去查。
  
  （目前百度有4台baidu.com的顶级域名服务器）。
  
  8.ISPDNS不厌其烦的再次向baidu.com这个域的权威服务器发起请求，baidu.com收到之后，查了下有www的这台主机，就把这个IP返回给你了，
  
  9.然后ISPDNS拿到了之后，将其返回给了客户端，并且把这个保存在高速缓存中
  ```

- 云服务商网络

  ```
  azure 虚拟网络：在虚拟网络中，运行常用网络虚拟设备（WAN 优化器、负载均衡器、应用程序防火墙）并定义通信流，从而在设计网络时拥有更高的控制力。
  路由网络流量
  默认情况下，Azure 在子网、连接的虚拟网络、本地网络以及 Internet 之间路由流量。 可使用以下两个选项中任意一个或同时使用二者替代 Azure 创建的默认路由：
  路由表： 可创建自定义路由表，其中包含可对每个子网控制流量路由到位置的路由。 详细了解路由表。
  边界网关协议 (BGP) 路由： 如果使用 Azure VPN 网关或 ExpressRoute 连接将虚拟网络连接到本地网络，则可将本地 BGP 路由传播到虚拟网络。 详细了解如何将 BGP 与 Azure VPN 网关和 ExpressRoute 配合使用。
  VNet 对等互连 - 连接同一 Azure 区域中的 VNet
  全局 VNet 对等互连 - 跨 Azure 区域连接 VNet
  无论是否与另一个虚拟网络建立对等互连，每个虚拟网络仍可具有自己的网关，并使用它连接到本地网络。 即使虚拟网络对等，用户也可以使用网关配置虚拟网络到虚拟网络连接。
  若已配置虚拟网络互连的两个选项，则虚拟网络之间的流量将通过对等配置（即通过 Azure 主干）流通。
  将虚拟网络对等互连后，还可以将对等虚拟网络中的网关配置为本地网络的传输点。 在这种情况下，使用远程网关的虚拟网络没有自己的网关。 一个虚拟网络只能有一个网关。 网关可以是本地网关或远程网关（对等虚拟网络中）
  
  创建对等的虚拟网络
  步骤 1 - 规划 IP 地址范围
  以下步骤将创建两个虚拟网络，以及它们各自的网关子网和配置。 然后在两个 VNet 之间创建 VPN 连接。 必须规划好网络配置的 IP 地址范围。 请记住，必须确保没有任何 VNet 范围或本地网络范围存在任何形式的重叠。
  步骤 2 - 创建并配置 TestVNet1
  步骤 3 - 创建并配置 TestVNet4
  步骤 3 - 创建并配置 TestVNet4
  
  ```

  

### K8S

```
etcd 一款开源软件。提供可靠的分布式数据存储服务，用于持久化存储K8s集群的配置和状态。
K8s API server 用户程序（如kubectl）、K8s其它组件之间通信的接口。K8s其它组件之间不直接通信，而是通过API server通信的。这一点在上图的连接中可以体现，例如，只有API server连接了etcd，即其它组件更新K8s集群的状态时，只能通过API server读写etcd中的数据。
Scheduler 排程组件，为用户应用的每一可部署组件分配工作结点。
Controller Manager 执行集群级别的功能，如复制组件、追踪工作结点状态、处理结点失败等。Controller Manager组件是由多个控制器组成的，其中很多控制器是按K8s的资源类型划分的，如Replication Manager（管理ReplicationController 资源），ReplicaSet Controller，PersistentVolume controller。
kube-proxy 在应用组件间负载均衡网络流量。
Kubelet 管理工作结点上的容器。
Container runtime Docker, rkt等实际运行容器的组
```

- 日志管理 

  ```
  # 日志级别： 基础日志 Node级别的日志 群集级别的日志架构
  
  在本文中采用使用Node日志记录代理的方面进行Kubernetes的统一日志管理，相关的工具采用：
  
  日志记录代理（logging-agent）：日志记录代理用于从容器中获取日志信息，使用Fluentd；
  日志记录后台（Logging-Backend）：日志记录后台用于处理日志记录代理推送过来的日志，使用Elasticsearch；
  日志记录展示：日志记录展示用于向用户显示统一的日志信息，使用Kibana。
  
  使用Filebeat收集Kubernetes的应用日志
  在进行日志收集的过程中，我们首先想到的是使用Logstash，因为它是ELK stack中的重要成员，但是在测试过程中发现，Logstash是基于JDK的，在没有产生日志的情况单纯启动Logstash就大概要消耗500M内存，在每个Pod中都启动一个日志收集组件的情况下，使用logstash有点浪费系统资源，经人推荐我们选择使用Filebeat替代，经测试单独启动Filebeat容器大约会消耗12M内存，比起logstash相当轻量级。
  
  ```

  

- 如何运行一个容器

  ```
  开发者开发一个应用后，打包Docker镜像，上传到Docker registry；然后编写一个yaml部署描述文件，以描述应用的结构和资源需求。开发者通过kubectl（或其它应用），将部署描述文件提交到API server，API server将部署需求更新到etcd。etcd在K8s管理结点中的作用相当于数据库，其它组件提交到API server的数据都存储于etcd。API server非常轻量，并不会直接去创建或管理Pod等资源，在多数场景下甚至不会去主动调用其它的K8s组件发出指令。其它组件通过建立和API server的长连接，监视关心的对象，监视到变化后，执行所负责的操作。
  ```

- 高可用部署

  ```
  K8s高可用部署中有3个管理结点。etcd自身是一个分布式数据存储系统，按照其多实例部署方案，结点只需在启动时知道其它结点的IP和端口号即可组成高可用环境。和通常的应用服务器一样，API Server是无状态的，可以运行任意多个实例，且彼此之间无需互相知道。为了能使kubectl等客户端和Kubelet等组件连接到健康的API Server、减轻单台API Server的压力，需使用基础架构提供的负载均衡器作为多个API Server实例的入口。如上图的部署方法，每个主结点上都运行了一个etcd实例，这样API Server只需连接本地的etcd实例即可，无需再使用负载均衡器作为etcd的入口。
  
      Controller Manager和Scheduler需要修改K8s集群，同时修改时可能引发并发问题。假设两个ReplicaSet Controller同时监视到需创建一个Pod，然后同时进行创建操作，就会创建出两个Pod。K8s为了避免这个问题，一组此类组件的实例将选举出一个leader，仅有leader处于活动状态，其它实例处于待命状态。Controller Manager和Scheduler也可以独立于API server部署，通过负载均衡器连接到多个API server实例。
  --------------------- 
  作者：gongxsh00 
  来源：CSDN 
  原文：https://blog.csdn.net/gongxsh00/article/details/79932136 
  版权声明：本文为博主原创文章，转载请附上博文链接！
  ```

- 存储

  ```
  存储分为本地存储（DAS），网络存储（NAS），存储局域网（SAN）和软件定义存储（SDS）四大类
  
  DAS就是本地盘，直接插到服务器上
  NAS是指提供NFS协议的NAS设备，通常采用磁盘阵列+协议网关的方式
  SAN跟NAS类似，提供SCSI/iSCSI协议，后端是磁盘阵列
  SDS是一种泛指，包括分布式NAS（并行文件系统），ServerSAN等
  
  Kubernetes中跟存储相关的概念有PersistentVolume （PV）和PersistentVolumeClaim（PVC），PV又分为静态PV和动态PV。动态PV需要引入StorageClass的概念,Kubernetes通过访问模式给存储分为三大类，RWO/ROX/RWX
  块存储通常只支持RWO，比如AWSElasticBlockStore，AzureDisk，有些产品能做到支持ROX，比如GCEPersistentDisk，RBD，ScaleIO等
  文件存储（分布式文件系统）支持RWO/ROX/RWX三种模式，比如CephFS，GlusterFS和AzureFile
  
  # 使用场景
  配置
  
  无论集群配置信息还是应用配置信息，其特点是并发访问，也就是前边提到的ROX/RWX，在不同集群或者不同节点，都能够访问同样的配置文件，分布式文件存储是最优选择。
  
  日志
  
  在容器场景中，日志是很重要的一部分内容，其特点是高吞吐，有可能会产生大量小文件。如果有日志分析场景，还会有大量并发读操作。分布式文件存储是最优选择。
  
  应用（数据库/消息队列/大数据）
  
  Kafka，MySQL，Cassandra，PostgreSQL，ElasticSearch，HDFS等应用，本身具备了存储数据的能力，对底层存储的要求就是高IOPS，低延迟。底层存储最好有数据冗余机制，上层应用就可以避免复杂的故障和恢复处理。以HDFS为例，当某个datanode节点掉线后，原有逻辑中，会选择启动新的datanode，触发恢复逻辑，完成数据副本补全，这段时间会比较长，而且对业务影响也比较大。如果底层存储有副本机制，HDFS集群就可以设置为单副本，datanode节点掉线后，启动新的datanode，挂载原有的pv，集群恢复正常，对业务的影响缩短为秒级。高性能分布式文件存储和高性能分布式块存储是最优选择。
  
  备份
  
  应用数据的备份或者数据库的备份，其特点是高吞吐，数据量大，低成本。文件存储和对象存储最优。
  综合应用场景，高性能文件存储是最优选择
  
  ```

  

- NODE

- POD

- FANNEL

- Service

  ```
  Kubernetes中的Service 是一个抽象的概念，它定义了Pod的逻辑分组和一种可以访问它们的策略，这组Pod能被Service访问，使用YAML （优先）或JSON 来定义Service，Service所针对的一组Pod通常由LabelSelector实现（参见下文，为什么可能需要没有 selector 的 Service）。
  
  可以通过type在ServiceSpec中指定一个需要的类型的 Service，Service的四种type:
  
  ClusterIP（默认） - 在集群中内部IP上暴露服务。此类型使Service只能从群集中访问。
  NodePort - 通过每个 Node 上的 IP 和静态端口（NodePort）暴露服务。NodePort 服务会路由到 ClusterIP 服务，这个 ClusterIP 服务会自动创建。通过请求 <NodeIP>:<NodePort>，可以从集群的外部访问一个 NodePort 服务。
  LoadBalancer - 使用云提供商的负载均衡器（如果支持），可以向外部暴露服务。外部的负载均衡器可以路由到 NodePort 服务和 ClusterIP 服务。
  ExternalName - 通过返回 CNAME 和它的值，可以将服务映射到 externalName 字段的内容，没有任何类型代理被创建。这种类型需要v1.7版本或更高版本kube-dnsc才支持
  ```

  

- POD自动扩容

  ```
  Horizontal Pod Autoscaling，简称HPA，是Kubernetes中实现POD水平自动伸缩的功能
  
  工作流程:
  1.创建HPA资源，设定目标CPU使用率限额，以及最大、最小实例数, 一定要设置Pod的资源限制参数: request, 负责HPA不会工作。
  2.控制管理器每隔30s(可以通过–horizontal-pod-autoscaler-sync-period修改)查询metrics的资源使用情况
  3.然后与创建时设定的值和指标做对比(平均值之和/限额)，求出目标调整的实例个数
  4.目标调整的实例数不能超过1中设定的最大、最小实例数，如果没有超过，则扩容；超过，则扩容至最大的实例个数
  重复2-4步
  
  
  自动伸缩算法: 
  HPA Controller会通过调整副本数量使得CPU使用率尽量向期望值靠近，而且不是完全相等．另外，官方考虑到自动扩展的决策可能需要一段时间才会生效：例如当pod所需要的CPU负荷过大，从而在创建一个新pod的过程中，系统的CPU使用量可能会同样在有一个攀升的过程。所以，在每一次作出决策后的一段时间内，将不再进行扩展决策。对于扩容而言，这个时间段为3分钟，缩容为5分钟(可以通过--horizontal-pod-autoscaler-downscale-delay, --horizontal-pod-autoscaler-upscale-delay进行调整)。
  
  HPA Controller中有一个tolerance（容忍力）的概念，它允许一定范围内的使用量的不稳定，现在默认为0.1，这也是出于维护系统稳定性的考虑。例如，设定HPA调度策略为cpu使用率高于50%触发扩容，那么只有当使用率大于55%或者小于45%才会触发伸缩活动，HPA会尽力把Pod的使用率控制在这个范围之间。
  具体的每次扩容或者缩容的多少Pod的算法为: Ceil(前采集到的使用率 / 用户自定义的使用率) * Pod数量)
  每次最大扩容pod数量不会超过当前副本数量的2倍
  
  ```

  

- HostAliases

  ```
  使用 HostAliases 向 Pod /etc/hosts 文件添加条目
  ```

  

- Kube-DNS

  ```
  介绍 Kubernetes 內部插件 kube-dns
  而 Kubernetes 本身提供了 DNS 的套件，kube-dns。 kube-dns 帮助在同一个 Kubernetes Cluster 中的所有 Pods ，都能透过 Service 的名称找到彼此。透过 kubectl get 指令，会发现 kube-dns 也是一个在 Cluster 中运行的服务，一旦 Kubernetes Cluster 被建立后，便会自动运行。
  
  而 kube-dns 的相关设定档则放是放在 master node 的 /etc/kubernetes/addons 资料夹底下，以 minikube 为例，minikube 运行的 VM 本身就是 master node，所以我们先透过 minikube ssh 指令登入，
  
   kube-dns 是运行在 Kubernetes Cluster 的一个 Pod，而这个 kube-dns-86f6f55dd5-cht2h Pod，也有一个相对应的 Service 物件。
   
   Kubernetes 在每一个 Pod 创建时，都会在该 Pod 的 /etc/resolve.conf 档案中，自动加入 kube-dns service 的 domain name 与相对应的 IP 位址。因此 其他 Pods 可以透过名称为 kube-dns 的 Service 物件，找到正在运行的 kube-dns
   
  使用CoreDNS进行服务发现
  上面我们使用的是kube-dns进行的dns管理,当然还有很多其他的dns管理工具, 用的多的就是CoreDNS.
  
  要使用CoreDN您的Kubernetes服务器必须是v1.9或更高版本
  
  https://blog.csdn.net/luanpeng825485697/article/details/84108166
  ```

  

### 技术选型

**维度** 

#### **目标产品**

这是最重要的维度。产品本身的特征将影响技术选型时的很多因素。

**短生命周期产品和长生命周期产品**

短生命周期的产品通常要求快速起步：门槛低、书写自由、不强制遵循任何最佳实践。当它的使命结束时，代码会被直接抛弃。所以，对于这类产品，“**快糙猛**”的技术是较好的选择，当然，能做到“**快精猛**”更佳。

而长生命周期的产品则会强烈要求可维护性，因为它们在很长时间内都是不可报废的。甚至对于一些生命线产品，连重写都会要求在重写期间线上系统平稳过渡，一点点迁移到新技术。

这种要求对团队的工程化能力是个极端的考验。如果没有相应的工程能力，其代价甚至会高于用新技术重新写一个功能相同的系统。

**探索型的产品和守成型的产品**

探索型产品往往也是短周期产品，但是同时也有自己的特点。它要求快速，但往往同时会要求高质量。探索型的产品如果证明了可行性，那么过渡到长生命周期的可能性很大。

这就要求它最好是一个微内核系统，提前留出一些扩展的空间。当然，设计微内核系统对架构师的能力具有相当的考验，如果没有一个优秀的架构师，建议还是不要刻意做任何预留，优先保障系统的简单性。

除此之外，探索型产品的技术栈必须支持可靠的、自动化的重构。因为探索型产品的迭代速度很快，如果完全靠人工去添加功能并手动重构，那么一旦出现 BUG，将给此产品的用户体验带来严重的负面影响。

所以，除非由于人才储备等原因而被迫做出折中，否则探索型产品的技术栈一定要快速而严谨。

当然，“**大力出奇迹**”定律也是成立的。也就是说，如果你有决心也有力量在将来对这个探索型产品进行彻底的重写，那么采用快糙猛的技术快速把它搭建起来，也未尝不可。如果你的业务确实能如预期般爆发，那么只要把重点放在系统延展性等方面即可；但是如果不能如预期般爆发，可能就会导致维护成本在中期开始飙升，在竞争中处于劣势。这是一种“不成功便成仁”的策略。据我所知某独角兽企业就是在业务起来之后通过巨额投入来偿还技术债的。但这对于 CTO 的技术直觉是一项极大的考验，不要轻易效仿。

而对守成型产品的选型则会侧重于与现有技术栈的相似程度和无缝整合能力。如果整合时需要借助很多技巧，那么可能你就是在给自己挖坑。

在引入新技术的过程中，要尽可能符合现有的开发流程、基础设施和开发习惯。当然，如果现有的这些已经严重过时，那么应该找新老技术的专家，共同帮你设计一个路线图，让你可以平稳地引入新技术，这份投资绝对值得。如果老技术已经有新版本，则应该优先考虑升级它。不要幻想换个技术栈就能解决一切问题，事实上，它带来的问题往往会更多。

**边缘产品和生命线产品**

在人员的学习能力和意愿允许的前提下，边缘产品是最佳的试验场，适合探索各种候选技术，试验各种激进方案，积累经验教训。其影响范围可控，即使失控也不会带来太大的损失。当然，即使探索，也应该有计划地探索，不要每个边缘产品都采用不同的技术方案，那样会给人才供应带来巨大的挑战。

而生命线产品则应该稳妥优先，采用保守方案。所以应该优先采用团队内部积累了一定经验或具有稳定的强力外援的技术。

所有的生命线产品几乎必然是长周期产品，所以其可维护性同样是重中之重。

**产品维度总结**

在目标产品维度上，低价值产品优先考虑门槛低的技术，但是高价值产品应该尽早进行投资性技术积累，优先考虑天花板高的技术，这样才不至于在若干年之后被迫重写。如果工程化能力不足，这种重写往往会成为灾难。

#### **目标用户**

用户的特点对于技术选型具有显著的影响，甚至可能会导致产品不可用。

**浏览器版本**

在前端领域，浏览器版本是永远的痛，但这是需要权衡的。高版本浏览器甚至是单一的低版本浏览器会显著节省开发成本，但是可能会损失一些用户。该怎么解决呢？当然不能拍脑袋决定。

如果你们已经有同领域的线上系统，那么应该统计这些线上系统的访问情况，得出一个最准确的、针对目标客户群的统计，然后分析一下不同版本的浏览器有多大价值，有没有可能通过非技术手段让用户使用你们的目标浏览器。即使没有线上系统，也可以随机对目标用户群发一些调查问卷，确定他们的实际使用情况，以及安装新版浏览器的可能性。

下下之策是查一下百度公布的全网浏览器数据，然后说“我们要支持某某浏览器，它还有 10% 市场占有率呢！”，这是懒。

**用户带宽**

同样是前端领域，文件的下载体积可能会被一些人当做亮点进行宣传，但是你要清楚，现在已经是 4G 时代了，更不用说很多企业内部应用都是千兆带宽。就算能比候选技术小 100k，在 4G 带宽下（假设现实带宽是 2MB/s）也就是 100 毫秒，有谁能感觉到这部分差异？ 这就是一个明显的“**误导读者**”的例子。

**可访问性**

在产品的用户群体中，不但有健康人，还有色盲以及盲人等残疾人。特别是对于面向消费者的产品，尽可能的考虑这些人的需求不但能体现出产品的“人文关怀”，而且也在一定程度上扩大客户群。比如苹果和微软等大公司都把可访问性放在了核心位置。如果你决定要实现可访问性，那么就应该把它作为一项需求，纳入到选型时要考虑的因素中。

之所以要把它纳入到技术选型过程中，是因为添加可访问性支持的代价比较高，而很多第三方库并没有提供这方面的支持。所以应该提早考虑。

**国际化**

与可访问性相似，国际化也是一个后期添加代价比较高，但很多候选技术却没有提供支持的特性。

如果你的产品在预期生命周期的相当一段时间内需要供多语言用户使用，那么，在初期选型时，就要把候选技术的国际化能力和质量纳入你的主要考量。

**访问频度**

用户的访问频度对前后端的技术选型都有很大影响。

比如说一个一年只用一次的功能，考虑其性能很可能是没有必要的，在一小时内跑完和在一分钟内跑完往往没有显著的价值差异。但是这两种技术方案却可能有着硬盘占用、编程复杂性、运维复杂性等方面的成本差异。你需要考虑：那种能在一分钟内跑完的技术是否能给你带来足够的价值。

对于前端来说，频繁访问的、面向消费者的应用通常会要求更高的流畅度，那么在技术选型时，就要选择流畅度更高的技术。但是这个流畅度一定要设计一个仿真的场景，亲自验证一下，甚至做一些灰度发布在现实场景下进行验证，而不要只看其官网宣称的流畅度。比如阿里的闲鱼团队就对 Flutter 技术进行了长时间的灰度验证，最终替换成了完全使用 Flutter 的版本，堪称对新技术进行选型的模范。

**用户维度总结**

要特别小心，不要根据错误的、片面的信息作出决策。很多第三方的技术选型指南背后都有着它们自己的场景，但大多数都不会给你写清楚，有的甚至复杂到想给你写清楚都做不到。甚至有些选型指南还有着强烈的主观立场，为了证明自己的预设立场甚至不惜造假。所以，你要先清点出你们的产品最应该重视的那些指标，然后拿这些指标对候选技术进行可行性测试，甚至为此专门开启一些 SPIKE 项目，而不要迷信第三方选型指南。

#### **目标团队**

目标团队的因素确实很重要，但并不像你认为的那么重要。除非你的人才供应真的有问题（难道不应该先反思一下是不是钱给少了？），否则应该优先考虑提升团队能力，而不是削足适履。

**技术背景**

目标团队的技术背景对新技术的选型确实很重要，但是没必要去精确匹配。

比如 Java 团队要做前端，选择 GWT 看似很好，但 GWT 也有自己的问题，几乎完全无法利用前端生态。他们更好的选择可能是 Angular：从语言上，TypeScript 跟 Java 有诸多相似之处；从架构模式上，对 MVC 的理解稍微往前推一步就是 Angular 的 MVVM 模式；从特性上，依赖注入不要太熟悉；从生态上，你可以自由决定是否使用前端生态，取长补短。

同样，前端团队如果打算自己写 BFF，也不一定非要在 Node 生态下打转。你完全可以使用 Java 世界的 Reactor 或者 WebFlux 进行响应式编程。这样可以和后端的其它 Java 体系更好地进行集成，并减少运维的复杂度。

**团队规模**

团队规模可能是团队维度中对技术选型影响最大的因素。

四位开发人员以下的小规模团队，如果大家都很专业，那么其沟通成本就很低，在技术选型上可以更倾向于选择灵活的技术，因为较高的人员能力和较低的沟通成本，可以让灵活的框架更好地发挥其作用，最终更加高效、高质量的推出产品。这种场景通常出现在由牛人组成的创业团队中。

如果开发人员经验不足或者做事不够专业，就需要更强的约束，特别是对于职场新鲜人，在早期养成好的开发习惯是非常重要的。而开发习惯中最重要的一点就是：约束 —— 知道不该做什么。这时候，偏向自由的技术可能会一时爽，但最终会构筑一个玻璃天花板，导致迟迟无法突破到下一个层次。

如果团队规模过大，那么首要的选择是用 DDD 等宏观技术把问题域细分，使其可以被小规模团队承接。如果暂时还做不到，就要考虑建设完善的基础设施和交付纪律，来为团队协作提供自动化保障。如果这些都做不到，就应该选择强约束性的具体技术，让大家避免犯错，或者尽早发现错误。在争取到时间之后，再逐渐深入化解根本性原因。

**组织架构**

康威定律深刻地影响着很多方面，技术选型也不例外。特别是做宏观技术选型时，必须考虑它在最终技术架构中的位置，以及与团队沟通结构的匹配程度。即使是一项很先进的技术，假如它与体系中的其它技术栈不匹配，也可能导致翻车。

当选择多个第三方库的时候更要加倍小心，因为它们开发时互相不知道彼此的存在，特别是对于一些较新的技术，可能都没人把它们搭配使用过。

除了开发架构之外，还要考虑更广泛的运维架构。假如你们引入了 DevOps，可能这个问题会得到一定程度的缓解。假如没有，那就要充分考虑上下游环节的人员能力和配套设施是否完备。比如如果运维部门缺乏 NodeJS 运维技能，就不要盲目引入基于 NodeJS 的后端，一定要拿到他们“**我能**”的承诺之后再开始。

除非你是个前后端 + DevOps 全栈，否则就需要尽早对组织架构方面的因素进行验证并排除风险。也就是说，在一个可控的演习环境中，用一个小型案例，完整地走一遍开发、上线、发新版的流程。在这个过程中，一些显著的风险将会暴露出来，要评估其影响，来决定如何选型。

**人员流动性**

人员流动带来的损失比大多数人所认为的要大得多。人员流动会带走知识和文化。企业要避免损失，就要把这些知识和文化尽可能记录在代码中。

当然，这并不意味着应该要求大量写注释，而应该使用那些能留存知识的技术，比如类型系统和规范化命名。类型系统和规范化命名可以半强制性地要求开发人员把原本只存在于自己脑子里的知识记录到代码中。如果更有追求一点，可以再尝试普及单元测试。这样，当他离开的时候，即使没有文档，这些知识也仍然能留存下来。从效果上说，代码往往比文档和注释更好。

而文化的留存则更加困难，事实上，代码中的奇葩注释往往留存的是负面文化。应该在代码中留存的文化，是严谨、专业的工作态度。虽然自由也是文化的一部分，甚至在管理领域是非常值得向往的文化，但在工程领域，它往往是一种负面文化，因为软件开发领域并没有公认的法律甚至道德。你可以想象一下管理领域中没有约束的自由会导致怎样的后果。

所以，要想应对人员流动的风险，除非你有信心留存知识与文化，否则就应该在技术选型时，倾向于选择更加严谨的、隐式信息更少的技术。

**团队维度总结**

鞋子好不好，只有脚知道。错误的选型，也只能由团队自身来承受。阿波罗神庙上镌刻着一句警世名言——了解你自己。所以，请先客观认识自己的团队，然后再据此进行选型，千万不要懒于思考，盲从潮流。

#### **技术本身**

对技术本身的考量，主要是代入其它维度之后，看其匹配程度。

技术本身在选型中可能反而是最不重要的一个维度。这些年的历史早已证明：优秀的技术未必能流行起来；很多技术的流行，也并非是由于其优秀。

**明确的定位**

一项优秀的技术，应该有其明确的定位和发展路线。这些定位能清楚地表明自己要做什么、不做什么。而其发展路线应该至少有一年以上的提前规划，而且在定位上要能与其前辈做出有效区隔，而不是亦步亦趋，没有自己的特长。

**代码质量**

虽然流行的未必优秀，优秀的也未必流行，但技术选型不是赶时髦。所以，在条件允许的情况下，还是应该尽可能选择优秀的技术。代码质量高的技术，将来技术本身由于维护成本飙升而被放弃的可能性也较小。

衡量代码质量的标准有很多，其中最常用、也比较有效的是单元测试的覆盖率。而那些从一开始就具有比较完备的单元测试的代码库，往往优于后补测试的代码库。因为这证明的是开发组的工程化能力和意识，而这些是该技术长期可维护性的根本保障。当然，除非该技术特别复杂或应用场景的容错性特别小，否则也不必苛求超过 90% 的覆盖率。

**维护团队**

维护团队的规模和能力，对于一项技术在长跑中的表现非常重要。在历史上如流星般划过的技术数不胜数，但最终能长期留下来的却不多。维护一项技术的成本远高于创建它，所以如果没有一个健康、可持续的商业模式，一个像 Linus 那样的志愿者，以及一个愿意出钱的超级大金主，那么它在未来的竞争中落败只是迟早的事。除非这项技术的需求集足够小而稳定，否则这些因素缺一不可。

**社区**

社区的质量，决定着这项技术长远的未来，一些草根型技术的隐患就在于此。如果社区人员的素质过低，喜欢无原则的站队，而不能理性的对该技术提出尖锐的意见甚至批评，那么这个社区迟早会衰落。这类社区有一个显著地特征就是喜欢宣扬它“**包治百病**”，也就是说它适合一切场景，而不会先问你一些问题再决定是否要推荐给你。另一个特征就是喜欢通过刻意选取某些标准来做出片面的对比，这种行为在学术界属于学术造假行为，但在我们工业界却被习以为常，这不能不说是我们的悲哀。

好的社区应该是一个君子社区。他们会自觉遵守共同的、理性的行为规范。会把精力放在对技术本身做贡献，而不是通过诡辩、群殴等手段来攻击竞争技术。社区的主要领导者会对社区的不良行为提出批评、做出约束，甚至为社区成员的不良行为道歉，而不是放任不管。

**技术维度总结**

不要把技术看得太重。对所有的主观性宣传文章，留一些心眼，多问一句——那缺点呢？将来决定你们是否会掉在坑里的，就是它的缺点。

对于那些会如实告诉你缺点的宣传文章，请高看一眼，因为作者是真的希望对你们团队的未来负责。

对于功利社区，请务必小心；对于君子社区，请自觉维护。

------

**反模式** 

有一些技术选型策略可能会导致灾难性的失败，这些选型中存在一些共同的反模式，比如：

#### **舆论驱动选型**

人云亦云，盲目听信外人或者某些布道师的主观性言论，这就是舆论驱动选型。它往往会带来灾难。

做任何决策时，如果要借助参考资料，请记住：最重要的不是它告诉了你什么，而是它对你隐瞒了什么，这些隐瞒的信息最终会置你于险境。

特别是当该资料的作者对某项技术具有显著的倾向性时，请深入想想，他向你推荐的每一项优点是否真的“**对你**”有价值，以及它背后的代价是什么。比如，推崇“**自由**”的技术往往不够“**严谨**”，如果你的产品需要严谨，那么请把“**自由**”看做减分项而不是加分项。比如，推崇“**体积小**”的技术在现在动辄几T硬盘、几M带宽的环境下，到底对你来说有多大价值？它是不是因为没有其它的优点了才把这种细枝末节亮出来吸引你？

即使是调查报告之类的客观参考资料，也需要了解其背景。比如一份只发给程序员的调查报告，可能会发现 Chrome 的使用率超过了 99%，但显然它对你的面向普通用户的产品毫无价值，只会给你带来风险。同时，要注意很多调查报告的设计是有主观倾向性的，甚至题目的排列顺序都会给最终结果带来 10% 以上的偏差。所以，一定要仔细分析其中立性、客观性以及调查对象在你的目标场景下的代表性。

#### **单一指标驱动选型**

根据任何一个单一指标进行选型都会给你带来灾难，更何况很多指标并不适合作为选型的依据。

有些指标很容易操纵，比如 GitHub 仓库上的 Star 就是很容易操纵的，在淘宝网上还有专门购买 GitHub Star 的服务，而 GitHub 的年度报告中也已经不再把 Star 作为主要指标使用。即使是那些不容易造假的指标，比如 commit 数量，其实也不适合作为主要指标使用，它可能意味着作者具有良好的工程习惯和足够勤奋，但也可能意味着代码库质量堪忧，因此不断推出补丁。

当然，有一些客观指标还是比较适合作为主要指标来使用的，但也不要盲目相信数字。比如单元测试中覆盖率较高的项目，确实通常质量比较好，但是我也见过一些只有调用却没有断言的测试，那些测试的覆盖率也会很高，但却是假的。所以，如果要评估其质量，最好还是亲自打开看一看。

即使你选出了一些主要指标，并且确信它们没有造假，也仍然不能简单地把它们加起来或加权平均来得出一个数字进行比较。你要综合评估这些指标对你的目标产品、目标用户、目标团队的价值。如果技术选型只是个数字游戏，那还要你干嘛？

#### **话语权驱动选型**

这几乎是最糟的选型，但却屡见不鲜。技术栈的更迭往往会带来话语权的变化，而这将给公司带来灾难。

对于高级技术决策者，需要有战略定力，应该以一种规范的、用事实说话的方式来控制技术选型的副作用。我曾见过一帮程序员“**偷袭珍珠港**”导致架构师被迫辞职的惨剧，我当时的意见是：这是 CTO 的锅。团队由于选择技术栈而产生了话语权之争，说明制度设计和文化建设出了大问题，这只能由 CTO 背锅。

所以，如果你是个技术决策者，那么应该尽早站出来，发挥你的职权和非职权影响力，抑制这些负面文化，而不是任由其发展，最终破坏公司的总体技术路线，甚至技术氛围。

#### **粉丝驱动选型**

对于生命线产品，最糟糕的选型莫过于粉丝驱动选型了，这次可没有“**几乎**”。对于技术人员来讲，最重要的特质是客观冷静，这样才能配得上“**专业**”二字。而拜大神，当作玩笑尚可，如果让它影响到你的决策，那么你就应该趁早隐退了，免得将来被迫引咎辞职。

虽然也曾被人称作“**大神**”，但我一般会提出反对，至少不作正面回应。我已工作二十多年，太清楚业界百态了。实际上，很少有人真的配得上大神的称号，举世可能只有 Anders Hejlsberg、Bob 大叔、Martin Fowler、Jeff Dean 等少数几位。不过我相信如果你当面叫他们大神，他们也会反感的。

就算是对于这些举世公认的大神，也不应该成为你技术选型的依据，顶多是相信他们会珍惜名誉、不会粗制滥造而已，因为即使是精品也仍然有着明确的适用范围，超出这个范围它也可能会成为毒药。

当然，对于边缘产品，进行粉丝驱动选型也未尝不可，甚至可能更好。只是得记住，要做就请做好，别给你的偶像丢脸，更不要做好之后就觉得公司一定要把它应用于生命线产品中。

### 性能优化

- 性能指标有哪些
- 如何发现性能瓶颈
- 性能调优的常见手段
- 说说你在项目中如何进行性能调优

## 工程篇

### 需求分析

- 你如何对需求原型进行理解和拆分
- 说说你对功能性需求的理解
- 说说你对非功能性需求的理解
- 你针对产品提出哪些交互和改进意见
- 你如何理解用户痛点

### 设计能力

- 说说你在项目中使用过的 UML 图
- 你如何考虑组件化
- 你如何考虑服务化
- 你如何进行领域建模
- 你如何划分领域边界
- 说说你项目中的领域建模
- 说说概要设计

### 设计模式

- 你项目中有使用哪些设计模式
- 说说常用开源框架中设计模式使用分析
- 说说你对设计原则的理解
- 23种设计模式的设计理念
- 设计模式之间的异同，例如策略模式与状态模式的区别
- 设计模式之间的结合，例如策略模式+简单工厂模式的实践
- 设计模式的性能，例如单例模式哪种性能更好。

### 业务工程

- 你系统中的前后端分离是如何做的
- 说说你的开发流程
- 你和团队是如何沟通的
- 你如何进行代码评审
- 说说你对技术与业务的理解
- 说说你在项目中经常遇到的 Exception
- 说说你在项目中遇到感觉最难Bug，怎么解决的
- 说说你在项目中遇到印象最深困难，怎么解决的
- 你觉得你们项目还有哪些不足的地方
- 你是否遇到过 CPU 100% ，如何排查与解决
- 你是否遇到过 内存 OOM ，如何排查与解决
- 说说你对敏捷开发的实践
- 说说你对开发运维的实践
- 介绍下工作中的一个对自己最有价值的项目，以及在这个过程中的角色


