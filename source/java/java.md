# JAVA知识

## S.O.L.I.D

S.O.L.I.D是面向对象设计和编程(OOD&OOP)中几个重要编码原则(Programming Priciple)的首字母缩写。

SRP	The Single Responsibility Principle  单一责任原则
OCP	The Open Closed Principle  开放封闭原则
LSP	The Liskov Substitution Principle	里氏替换原则
DIP	The Dependency Inversion Principle	依赖倒置原则
ISP	The Interface Segregation Principle	接口分离原则

## **java IO**

### 主要内容

- **java.io.File类的使用**
- **IO原理及流的分类**
- **文件流**
- **FileInputStream / FileOutputStream / FileReader / FileWriter**
- **缓冲流**
  - **BufferedInputStream / BufferedOutputStream /**
  - **BufferedReader / BufferedWriter**
- **转换流**
- **InputStreamReader / OutputStreamWriter**
- **标准输入/输出流**
- **打印流（了解）**
- **PrintStream / PrintWriter**
- **数据流（了解）**
- **DataInputStream / DataOutputStream**
- **对象流 ----涉及序列化、反序列化**
- **ObjectInputStream / ObjectOutputStream**
- **随机存取文件流**
- **RandomAccessFile**

### File类

- **java.io.File类：文件和目录路径名的抽象表示形式，与平台无关**
- **File 能新建、删除、重命名文件和目录，但 File 不能访问文件内容本身。如果需要访问文件内容本身，则需要使用输入/输出流。**
- **File对象可以作为参数传递给流的构造函数**
- **File类的常见构造方法：**
  - **public File(String pathname)**

以pathname为路径创建File对象，可以是绝对路径或者相对路径，如果pathname是相对路径，则默认的当前路径在系统属性user.dir中存储。

- **public File(String parent,String child)**

以parent为父路径，child为子路径创建File对象。

- File的静态属性String separator存储了当前系统的路径分隔符。
- 在UNIX中，此字段为'/'，在Windows中，为'\\'

常见方法：

![img](https://images0.cnblogs.com/blog/651900/201412/172221382817208.png)

eg：



### Java IO原理

- IO流用来处理设备之间的数据传输。
- Java程序中，对于数据的输入/输出操作以"流(stream)" 的方式进行。
- java.io包下提供了各种"流"类和接口，用以获取不同种类的数据，并通过标准的**方法**输入或输出数据。

![img](https://images0.cnblogs.com/blog/651900/201412/172221391566108.png)

![img](https://images0.cnblogs.com/blog/651900/201412/172221397033911.png)

#### 流的分类

- 按操作**数据单位**不同分为：**字节流(8 bit)，字符流(16 bit)**
- 按数据流的**流向**不同分为：**输入流，输出流**
- 按流的**角色**的不同分为：**节点流，处理流**

| **(抽象基类)** | **字节流**       | **字符流** |
| -------------- | ---------------- | ---------- |
| **输入流**     | **InputStream**  | **Reader** |
| **输出流**     | **OutputStream** | **Writer** |

1. Java的IO流共涉及40多个类，实际上非常规则，都是从如上4个抽象基类派生的。
2. 由这四个类派生出来的子类名称都是以其父类名作为子类名后缀。
3. 字节流：以byte为单位传输
4. 字符流：以char为单位传输

#### IO流体系

![img](https://images0.cnblogs.com/blog/651900/201412/172221401562281.png)

#### InputStream & Reader

- InputStream 和 Reader 是所有**输入流**的基类。
- InputStream（典型实现：**FileInputStream**）
  - int read()
  - **int read(byte[] b)**
  - int read(byte[] b, int off, int len)
- Reader（典型实现：**FileReader**）
  - int read()
  - **int read(char [] c)**
  - int read(char [] c, int off, int len)
- **程序中打开的文件 IO 资源不属于内存里的资源，**垃圾回收机制无法回收该资源，所以应该**显式关闭文件 IO 资源**。

#### OutputStream & Writer

- OutputStream 和 Writer 也非常相似：
  - **void write(int b/int c);**
  - **void write(byte[] b/char[] cbuf);**
  - **void write(byte[] b/char[] buff, int off, int len);**
  - **void flush();**
  - **void close();** 需要先刷新，再关闭此流
- **因为字符流直接以字符作为操作单位，所以 Writer 可以用字符串来替换字符数组，即以 String 对象作为参数**
  - **void write(String str);**
  - **void write(String str, int off, int len);**

#### 文件流

**读取文件**

1.建立一个流对象，将已存在的一个文件加载进流。

- **FileReader fr = new FileReader("Test.txt");**

2.创建一个临时存放数据的数组。

- **char[] ch = new char[1024];**

3.调用流对象的读取方法将流中的数据读入到数组中。

- **fr.read(ch);**



 

**写入文件**

1.创建流对象，建立数据存放文件

- **FileWriter fw = new FileWriter("Test.txt");**

2.调用流对象的写入方法，将数据写入流

- **fw.write("text");**

3.关闭流资源，并将流中的数据清空到文件中。

- **fw.close();**



 

注意点：

- 定义文件路径时，注意：可以用"/"或者"\\"。File.separator()
- 在写入一个文件时，如果目录下有同名文件将被覆盖。
- 在读取文件时，必须保证该文件已存在，否则出异常。

 

#### 处理流之一：缓冲流

- 为了提高数据读写的速度，Java API提供了带缓冲功能的流类，在使用这些流类时，会创建一个内部缓冲区数组

- 根据数据操作单位可以把缓冲流分为：

- **BufferedInputStream 和 BufferedOutputStream**

- **BufferedReader 和 BufferedWriter**

- 缓冲流要"套接"在相应的节点流之上，对读写的数据提供了缓冲的功能，提高了读写的效率，同时增加了一些新的方法

- 对于输出的缓冲流，写出的数据会先在内存中缓存，使**用flush()将**会使内存中的数据立刻写出

   



#### 处理流之二：转换流

- 转换流提供了在字节流和字符流之间的转换
- Java API提供了两个转换流：
  - **InputStreamReader和OutputStreamWriter**
- 字节流中的数据都是字符时，转成字符流操作更高效。

#### InputStreamReader

- 用于将字节流中读取到的字节按指定字符集解码成字符。需要和InputStream"套接"。
- 构造方法
- **public InputStreamReader(InputStream in)**
- **public InputSreamReader(InputStream in,String charsetName)**

如： Reader isr = new

InputStreamReader(System.in,"ISO5334_1");//指定字符集

#### OutputStreamWriter

- 用于将要写入到字节流中的字符按指定字符集编码成字节。需要和OutputStream"套接"。
- 构造方法
- **public OutputStreamWriter(OutputStream out)**
- **public OutputStreamWriter(OutputStream out,String charsetName)**

![img](https://images0.cnblogs.com/blog/651900/201412/172221405009553.png)



#### 补充：字符编码

- **编码表的由来**

计算机只能识别二进制数据，早期由来是电信号。为了方便应用计算机，让它可以识别各个国家的文字。就将各个国家的文字用数字来表示，并一一对应，形成一张表。这就是编码表。

- **常见的编码表**
- **ASCII**：美国标准信息交换码。
  - 用一个字节的7位可以表示。
- **ISO8859-1：**拉丁码表。欧洲码表
  - 用一个字节的8位表示。
- **GB2312：**中国的中文编码表。
- **GBK：**中国的中文编码表升级，融合了更多的中文文字符号。
- U**nicode：**国际标准码，融合了多种文字。
  - 所有文字都用两个字节来表示,Java语言使用的就是unicode
- **UTF-8：**最多用三个字节来表示一个字符。
- **编码：字符串à字节数组**
- **解码：字节数组à字符串**
- **转换流的编码应用**
- 可以将字符按指定编码格式存储。
- 可以对文本数据按指定编码格式来解读。
- 指定编码表的动作由构造器完成。

#### 处理流之三：标准输入输出流

- **System.in和System.out**分别代表了系统标准的输入和输出设备
- 默认输入设备是键盘，输出设备是显示器
- System.in的类型是InputStream
- System.out的类型是PrintStream，其是OutputStream的子类FilterOutputStream 的子类
- 通过System类的setIn，setOut方法对默认设备进行改变。
  - public static void **setIn**([InputStream](mk:@MSITStore:D:\API\JDK_API_1.6_zh_中文.CHM::/java/io/InputStream.html) in)
  - public static void **setOut**([PrintStream](mk:@MSITStore:D:\API\JDK_API_1.6_zh_中文.CHM::/java/io/PrintStream.html) out)

 



#### 处理流之四：打印流（了解）

- 在整个IO包中，打印流是输出信息最方便的类。
- **PrintStream(字节打印流)**和**PrintWriter(字符打印流)**
  - 提供了一系列重载的print和println方法，用于多种数据类型的输出
  - PrintStream和PrintWriter的输出不会抛出异常
  - PrintStream和PrintWriter有自动flush功能
  - System.out返回的是PrintStream的实例

 



 

#### 处理流之五：数据流（了解）

- 为了方便地操作Java语言的基本数据类型的数据，可以使用数据流。
- 数据流有两个类：(用于读取和写出基本数据类型的数据）
  - **DataInputStream** 和 **DataOutputStream**
  - **分别"套接"在 InputStream 和 OutputStream 节点流上**
- **DataInputStream中的方法**

boolean readBoolean()        byte readByte()

char readChar()            float readFloat()

double readDouble()        short readShort()

long readLong()            int readInt()

String readUTF() void readFully(byte[] b)

- **DataOutputStream中的方法**
- 将上述的方法的read改为相应的write即可。

 



#### 处理流之六：对象流

- **ObjectInputStream和OjbectOutputSteam**
- 用于存储和读取**对象**的处理流。它的强大之处就是可以把Java中的对象写入到数据源中，也能把对象从数据源中还原回来。
- **序列化(Serialize)：**用ObjectOutputStream类将一个Java对象写入IO流中
- **反序列化(Deserialize)：**用ObjectInputStream类从IO流中恢复该Java对象
- ObjectOutputStream和ObjectInputStream不能序列化static和transient修饰的成员变量

#### 对象的序列化

- **对象序列化机制**允许把内存中的Java对象转换成平台无关的二进制流，从而允许把这种二进制流持久地保存在磁盘上，或通过网络将这种二进制流传输到另一个网络节点。当其它程序获取了这种二进制流，就可以恢复成原来的Java对象
- 序列化的好处在于可将任**何实现了Serializable接**口的对象转化为**字节数据**，使其在保存和传输时可被还原
- 序列化是 RMI（Remote Method Invoke – 远程方法调用）过程的参数和返回值都必须实现的机制，而 RMI 是 JavaEE 的基础。因此序列化机制是 JavaEE 平台的基础
- 如果需要让某个对象支持序列化机制，则必须让其类是可序列化的，为了让某个类是可序列化的，该类必须实现如下两个接口之一：
  - **Serializable**
  - Externalizable
- 凡是实现Serializable接口的类都有一个表示序列化版本标识符的静态变量：
  - **private static final long serialVersionUID;**
  - serialVersionUID用来表明类的不同版本间的兼容性
  - 如果类没有显示定义这个静态变量，它的值是Java运行时环境根据类的内部细节自动生成的。若类的源代码作了修改，serialVersionUID 可能发生变化。故建议，显示声明
- 显示定义serialVersionUID的用途
  - 希望类的不同版本对序列化兼容，因此需确保类的不同版本具有相同的serialVersionUID
  - 不希望类的不同版本对序列化兼容，因此需确保类的不同版本具有不同的serialVersionUID

#### 使用对象流序列化对象

- 若某个类实现了 Serializable 接口，该类的对象就是可序列化的：
  - **创建一个 ObjectOutputStream**
  - **调用 ObjectOutputStream 对象的 writeObject(对象) 方法输出可序列化对象。注意写出一次，操作flush()**
- 反序列化
  - **创建一个 ObjectInputStream**
  - **调用 readObject() 方法读取流中的对象**
- **强调：**如果某个类的字段不是基本数据类型或 String 类型，而是另一个引用类型，那么这个引用类型必须是可序列化的，否则拥有该类型的 Field 的类也不能序列化

 

序列化:将对象写入到磁盘或者进行网络传输。

要求对象必须实现序列化

ObjectOutputStream oos = new ObjectOutputStream(new FileOutputStream("test3.txt"));

Person p = new Person("韩梅梅",18,"中华大街",new Pet());

oos.writeObject(p);

oos.flush();

oos.close();

//反序列化：将磁盘中的对象数据源读出。

ObjectInputStream ois = new ObjectInputStream(new FileInputStream("test3.txt"));

Person p1 = (Person)ois.readObject();

System.out.println(p1.toString());

ois.close();

 

#### RandomAccessFile 类

- RandomAccessFile 类支持 "随机访问" 的方式，程序可以直接跳到文件的任意地方来**读、写文件**
  - 支持只访问文件的部分内容
  - 可以向已存在的文件后追加内容
- RandomAccessFile 对象包含一个记录指针，用以标示当前读写处的位置。RandomAccessFile 类对象可以自由移动记录指针：
  - **long getFilePointer()：获取文件记录指针的当前位置**
  - **void seek(long pos)：将文件记录指针定位到 pos 位置**
- **构造器**
  - public **RandomAccessFile**([File](mk:@MSITStore:D:\API\JDK_API_1.6_zh_中文.CHM::/java/io/File.html) file, [String](mk:@MSITStore:D:\API\JDK_API_1.6_zh_中文.CHM::/java/lang/String.html) mode)
  - public **RandomAccessFile**([String](mk:@MSITStore:D:\API\JDK_API_1.6_zh_中文.CHM::/java/lang/String.html) name, [String](mk:@MSITStore:D:\API\JDK_API_1.6_zh_中文.CHM::/java/lang/String.html) mode)
- 创建 RandomAccessFile 类实例需要指定一个 mode 参数，该参数指定 RandomAccessFile 的访问模式：
  - **r: 以只读方式打开**
  - **rw：打开以便读取和写入**
  - **rwd:打开以便读取和写入；同步文件内容的更新**
  - **rws:打开以便读取和写入；同步文件内容和元数据的更新**

 

**读取文件内容**



**写入文件内容**

 



**流的基本应用小节**

- 流是用来处理数据的。
- 处理数据时，一定要先明确**数据源**，与**数据目的地**
  - 数据源可以是文件，可以是键盘。
  - 数据目的地可以是文件、显示器或者其他设备。
- 而流只是在帮助数据进行传输,并对传输的数据进行处理，比如过滤处理、转换处理等。

 

 

- **字节流-缓冲流（重点）**
- 输入流InputStream-FileInputStream-BufferedInputStream
- 输出流OutputStream-FileOutputStream-BufferedOutputStream
- **字符流-缓冲流（重点）**
- 输入流Reader-FileReader-BufferedReader
- 输出流Writer-FileWriter-BufferedWriter
- **转换流**
- InputSteamReader和OutputStreamWriter
- **对象流**ObjectInputStream和ObjectOutputStream（难点）
- 序列化
- 反序列化
- **随机存取流**RandomAccessFile**（掌握读取、写入）**


## Java线程上下文加载器与SPI

### SPI机制

SPI的全名为Service Provider Interface.大多数开发人员可能不熟悉，因为这个是针对厂商或者插件的。在java.util.ServiceLoader的文档里有比较详细的介绍。简单的总结下java spi机制的思想。我们系统里抽象的各个模块，往往有很多不同的实现方案，比如日志模块的方案，xml解析模块、jdbc模块的方案等。面向的对象的设计里，我们一般推荐模块之间基于接口编程，模块之间不对实现类进行硬编码。一旦代码里涉及具体的实现类，就违反了可拔插的原则，如果需要替换一种实现，就需要修改代码。为了实现在模块装配的时候能不在程序里动态指明，这就需要一种服务发现机制。 java spi就是提供这样的一个机制：为某个接口寻找服务实现的机制。有点类似IOC的思想，就是将装配的控制权移到程序之外，在模块化设计中这个机制尤其重要。

### SPI具体约定

java spi的具体约定为:当服务的提供者，提供了服务接口的一种实现之后，在jar包的META-INF/services/目录里同时创建一个以服务接口命名的文件。该文件里就是实现该服务接口的具体实现类。而当外部程序装配这个模块的时候，就能通过该jar包META-INF/services/里的配置文件找到具体的实现类名，并装载实例化，完成模块的注入。 基于这样一个约定就能很好的找到服务接口的实现类，而不需要再代码里制定。jdk提供服务实现查找的一个工具类：java.util.ServiceLoader

### 应用场景

common-logging：apache最早提供的日志的门面接口。只有接口，没有实现。具体方案由各提供商实现， 发现日志提供商是通过扫描 META-INF/services/org.apache.commons.logging.LogFactory配置文件，通过读取该文件的内容找到日志提工商实现类。只要我们的日志实现里包含了这个文件，并在文件里制定LogFactory工厂接口的实现类即可。
JDBC：jdbc4.0以前， 开发人员还需要基于Class.forName("xxx")的方式来装载驱动，jdbc4也基于spi的机制来发现驱动提供商了，可以通过META-INF/services/java.sql.Driver文件里指定实现类的方式来暴露驱动提供者.

### 线程上下文类加载器

线程上下文类加载器（context class loader）是从JDK 1.2开始引入的。类java.lang.Thread中的方法 getContextClassLoader() 和 setContextClassLoader(ClassLoader cl) 用来获取和设置线程的上下文类加载器。

如果没有通过 setContextClassLoader(ClassLoader cl) 方法进行设置的话，线程将继承其父线程的上下文类加载器。Java 应用运行的初始线程的上下文类加载器是系统类加载器。在线程中运行的代码可以通过此类加载器来加载类和资源。

为了加载类，Java还提供了很多服务提供者接口（Service Provider Interface，SPI），允许第三方为这些接口提供实现。那类加载就会存在问题：SPI 的接口是 Java 核心库的一部分，是由引导类加载器来加载的；SPI 实现的 Java 类一般是由系统类加载器来加载的。引导类加载器是无法找到 SPI 的实现类的，因为它只加载 Java 的核心库。在 SPI 接口的代码中使用线程上下文类加载器，就可以成功的加载到 SPI 实现的类。java的双亲委托类加载机制（ClassLoader A -> System class loader -> Extension class loader -> Bootstrap class loader）可以保证核心类的正常安全加载。但是右边的 Bootstrap class loader 所加载的代码需要反过来去找委派链靠左边的 ClassLoader A 去加载东西的时候，就需要委派链左边的 ClassLoader 设置为线程的上下文加载器即可。