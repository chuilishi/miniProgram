# Java

### 迭代器

以for为例 for e in  a对象

1. 调用a的__ iter __方法 ( 有这个方法就是可迭代对象Iterator )
2. 调用a的__ next __方法 ( 同时有这两个方法就是迭代器 )
3. 列表不是迭代器,但是是可迭代对象
4. next方法返回的是



### isinstance(东西,类型)

判断类型 



### 集合

get( index )获取

reverse( )顺序倒转

shuffle() 打乱

unmodifiableList() 传入一个collection,返回一个只读的list

swap( list , index1, index2 ) 将数组index1和index2上的数据交换

indexOf( 数据 ) 数组中数据的index

disjoint( ) 比较两个数组,一样返回true

toArray  Set转为list

removeAll( 集合 ) 从一个集合中移出另一个集合的东西

Collections.addAll( 数组1, 数组2 ) 将数组2的东西加到数组1中( 或者其他Collection)

Set、List、Map 的.of( )方法 创建不可变集合

### 栈,队列

Stack 栈  先进后出

Queue 队列 先进先出 ( java 中没有)

PriorityQueue 优先队列 PriorityQueue是**线程不安全**的，PriorityBlockingQueue是**线程安全**的. 

优先队列是带有优先级的队列 按照优先级出,高的会先出

 ### stackTrace

堆栈跟踪

StackTraceElement[] stackTraceElements = **Thread**.currentThread().getStackTrace();

可以返回当前的函数调用栈

每个对象都有函数的信息

### 异常

try{ 要监测的代码块 }

catch( Exception e ){ 执行 } ( e即是其类型 )

Exception 是所有可捕获的异常的最终父类 ( common ancestor)( 所以这段代码能捕获任何Exception )

分为Runtime_Exception 和non_Runtime_Exception 两个大类`

下面再分.

自己抛出异常: throw new Exception1( ) 然后会层层往上抛直到JVM,JVM将程序终止或者被catch到.



### OOP

调用原始方法: super.method( )



方法可以重名, 不能名字和参数类型一模一样



### 接口:interface

如果一个类 implements了一个接口, 那么这个接口就给了一个"**应该实现什么方法**"的规定 , 即是对行为的抽象

方法自己用@override重写



**接口中所有类都是抽象方法,相当于给用这个接口的类一个规范**

接口强调**特定功能的实现,抽象类 ** **强调所属关系**



接口的值都是public static final

接口的方法都是 public abstract ,而且都不能有大括号( 因为只是模板 )



一个接口可以extends多个接口



public interface Jumping{ 

​		public void( )jump;

}

public class cat **implements** Jumping{  ( cat 类是Jumping接口的实现 )

​	@override

}



抽象类可以作为返回值和形参



**接口的默认方法,静态方法,私有方法**

defalt 修饰的,默认方法  可以实现也可以不实现

static,private 就像类中的方法一样



### 内部类

内部的类可以直接访问外部类的数据( private也可以 ),外部类不能直接访问内部类.

Outer.inner a=new Outer( ) . new inter( )

局部内部类: 藏在方法里面定义的类.

**匿名类**

new  Dog(){

​		public String getName(){}

​		public int getAge{}

}

这就是一个继承Dog类的匿名类,

有一些函数需要传入Dog, 只是为了调用Dog的一些方法,这时我们这样创建一个一次性的类,比较省代码.

public void bark( Dog d){

​		System.out.println( d.getName)

}

这样的,把类当做函数用的,就可以临时创建一个扔给它.



### System

exit( 退出代码 ) ( 一般0 是正常退出 )

### 泛型

类的类型

class aaa  < T >{

​		public void show( T  t){

​			System.out.println( t.getName);

​	}

}

这里的T可以是任何类型,在定义的时候就可以写清楚

使得同一个类可以处理不同类型数据

比如 show ( t )  这里t可能是任何类,不可能对每个类都写一遍show方法,用泛型就简单多了

比如 ArrayList < Integer >a  一个数组可能传入很多种



##### 泛型的主要目的之一就是用来指定容器，而由编译器来保证类型的正确性。(就是说编译阶段就检查出来了,如果用object会运行时报错,因为本来类型就不确定)

##### 

**通配符** ?

List< ? > list1 =new ArrayList < Number >( ); ( 比object更通用 )

List< ? extends Number > list1 =new ArrayList < Number >( );

 ( 继承number,也就是只能填Number或Number的子类 )

List< ? super Integer >list1 = new ArrayList< Number > 

( super Integer 也就是只能填自己或父类)



### 可变参数

public static int sum ( **int... a**){ }

这样就可以传入任意多个参数,

参数被打包成名字为a 的数组



如果还想直接获得几个参数:

public static int sum ( **int b** , **int... a**){ }

把那几个特殊的放到前面, 这样编译器才好确认你要几个特殊的



Arrays.asList( ) 方法就用了可变参数来实现,可以用来赋初值 ( 这样形成的list大小不可变,也就是不能用add和remove )



### File

是文件和目录路径名的抽象表示 ( 可以理解为是一个字符串 )

直接传整个路径:

File f1 = new File( "E:\ \ programfile\ \ dgut" );  ( \ 是转义 字符)

打印f1,得到 E:\ programfile\ dgut 仅仅只是一个

传父路径和子路径:

File f1 = new File( "E:\ \ programfile", "dgut" ); 

传File对象也是没问题的: ( 毕竟相当于一个字符串 )

File f1 = new File( "E:\ \ programfile"); 

File f2 = new File( f1, "dgut" );

**File类的方法**

createNewFile( ) 如果没有,创建一个新空文件,返回true ( 已经有了返回false )

mkdir( ) 创建一个该路径的文件夹 ( 没有参数,创建的就是该对象的内容 )

mkdirs( ) 创建多级的目录 ( mkdir如果没有父目录就会返回false ,这个不会)

还有一些:

![image-20230111120322476](C:\Users\zh148\AppData\Roaming\Typora\typora-user-images\image-20230111120322476.png)



### I/O

字节流:除了处理字符的流都是字节流.

InputStream和OutputStream两个大类

下面再划分FileInputStream等等



FileOutputStream fos = new FileOutputStream( c:\ \Users \ \fos.txt )

1. 创建了文件
2. 创建了字节输出流对象fos
3. 让fos指向了fos.txt,搭建了传输通道

 **方法**

fos.write() 要输入的字节信息 ( 相当于打二进制数据进去,只不过是用十进制打 )

fos.write( 97 ) txt中会显示a ( 具体的去学习一下文件的表示)   

//这里也可以用write( "a".getBytes( ) ) 方法,该方法返回一个字符数组



fos.write( byte[]b ) 字节数组写入

fos.write( byte[]b ,index ,length ) 从index开始写length长的数据

注意如果write的最后一个参数是true,将在文件末尾写入,否则就是直接写在文件开头



fos.close( ) 关闭流,节约资源

在异常处理中,close操作放到finally中,永远要释放资源

想刷新流的内容,用flush( )



字符流:

FileReader()

FileWriter()



几个特别的方法:

readLine: 读一行.

newLine: 换一行



缓冲流:

- 字节缓冲流：BufferedInputStream，BufferedOutputStream
- 字符缓冲流：BufferedReader，BufferedWriter

BufferedInputStream bis=new BufferedInputStream ( new FileInputStream( ));

括号里面放上正常的输入流,然后就不用管了,直接用bis的write.

close的时候只需要close一个流就行



ObjectOutputStream与ObjectInputStream

将一个**序列化**后的对象读和写.

序列化只需要implements Serializable接口,且不需要重写任何方法.

( 因为是一个标识性质的接口 )

一旦有序列化标识,我们就会在读和写的时候检查这个对象的serialVersionUID,

这个是java综合该类的各方面信息生成的一个该对象的辨识符( 当然最好自己创建一个 )

当本地的类和input下来的对象之间冲突了,就报错,保证这个对象是自己这个类的.



使用方法:

类似BufferedInputStream ,创建时传一个基本的流进去.

ObjectOutputStream oos = new ObjectOutputStream ( new FileOutputStream( 路径 ) );



out的方法: writeObject( 对象 )

input的方法 readObject( 对象 )

readObject的时候返回一个Object,还要向下转型.

Object obj = ois.readObject( );

Student s =( Student )obj



### Properties类:

一种字典, 一般用来作为配置信息

我们在很多**需要避免硬编码的应用场景**下需要使用properties文件来加载程序需要的配置信息，比如JDBC、MyBatis框架等。Properties类则是properties文件和程序的**中间桥梁**，不论是从properties文件**读取信息还是写入信息**到properties文件都要经由Properties类

* 遍历:

Set s = properties.KeySet( );  //KeySet 相当于map的KeySet  ,还有一个values( )方法是取值

for( Object key : s){

​		properties.get( key );

}

* 赋值: 

setProperty( key,value ) //都得是字符串

* 根据键取值( 类似get ) 



与map区别: 不能指定泛型

**properties读取和写入**

Properties p = new Properties ( )  //然后setproperty了很多数据

p.store( 一个FileWriter对象 ,额外信息(没有写null))

p.load( 一个FileReader对象) 

注意,读取的文件格式如下:

```
pen=pilot
height=199// 每一行都是一个键值对
所以通过load方法很轻松地将配置文件转换成字典
```



### 线程

单线程: 所有程序按顺序执行  //一个进程只有一条执行路径

多线程:程序同步进行

多线程资源共享: 用同样的一块资源运行程序

冲突: 同时需要一部分资源了

线程同步: 用一些方法来保证不会冲突,

锁:synchronized 



### 创建线程

1. 将一个类声明为Thread的子类,重写其run方法,就能分配并启动子类的实例

启动线程: start( ) ( 仅仅调用run是不能启动线程的 )

2. 随便一个类,实现Runnable接口,然后重写run方法( 这就有成为线程的潜力了 )

   然后这样: Thread t= new Thread( 上面那个类 ) 这样t.start( )就启动.

3. 第一种偏向于直接创建一个进程, 第二种可以创建多个同一个类的线程.

启动后自动调用里面的方法

线程自动命名:Thread-0,Thread-1,以此类推

获取名称: getName( )

设置名称: setName( )

也可以创建类的时候设置一个构造方法

public Thread( name ){

​		super( name ); ( Thread的构造方法中有name )

}



获取正在进行的线程名称:

Thread.currentThread( ).getName( )

**线程调度**

Java中, 优先级高的线程先获得资源

getPriority( )获取线程优先级

setPriority( )设置线程优先级 ( 默认是5,最小1,最大10 )

**注意**线程高不代表一定在前面运行,只是获得cpu时间片的几率大



几个线程调度相关方法:

* **sleep**( 毫秒 )线程过了多少毫秒之后再执行一次

* **join**( )只有调用该方法的线程死了才会再调用其他方法

* **setDaemon**( )将该线程设置为守护线程, 即守护主线程进行.如果所有主线程死亡,守护线程消失

* **Lock锁** 

  private Lock lock= new  ReentrantLock( );   创建锁

  try{

  ​	lock.lock( )

  ​	xxx函数

  }

  finally{   lock.unlock( )  }

  这样以一种可见的形式将中间锁起来.  用try和finally是防止中间出问题后一直锁着

* **等待和唤醒/生产者消费者模式** 

  wait( ) 当前线程等待

  notify( ) 唤醒某个线程

  notifyAll ( ) 唤醒所有线程

  这样可以实现一个共享数据的地方,当生产者改变数据时去唤醒消费者,

  当消费者取完数据的时候就等待

  

  存储数据的类 Box 提供put和get方法

  生产者和消费者创建参数为 Box b 的构造函数,这样就可以传进来一个Box

  然后调用put和get方法





* **同步代码块:synchronized**

  1. Object o=new Object( )   

  然后用synchronized( o ){ } 将同时操作共享数据的危险代码放进来 

  ( 在这个操作对应的类里面,而不是main函数里面 )

  括号里面其实应该放一把锁,  但是由于java中每个对象都是一把锁,所以可以随便创建一个.  还要注意不能在括号里面直接new, 这样会反复创建锁,这样{}内用的就不是一把锁.

  2. 直接加到方法前面:

     public void synchronized func( ){ }

     如果该函数是非static的,该函数就被 **this** 上锁了

     如果该函数是static的,该函数被  **类名.class**上锁( 该类对应的字节码对象 )

     

#### 线程安全的类

vector: 使用方式与ArrayList几乎一样

StringBuffer: 一个带缓冲区的,长度可变的String.可以在字符串末尾追加,也可以删除

ConcurrentHashtable: 升级版Hashmap .hashmap是线程不安全的,这个是高性能

hashmap的实现 . 将内部分为很多Segment ,只有同一Segment并发写入才会触发锁

大部分时间不会.



#### 题外话

为什么静态方法不能访问非静态变量?

静态方法是随着类加载一起加载的, 非静态变量是等一切底层加载完毕后才开始加载.

假如访问可能会出现该值尚未加载的情况.



## 网络编程

* ip 每台计算机在网络中的标识号,通过标识指定计算机

* 端口 :每个程序在该设备中的标识, 通过标识指定程序
* 协议 :传输时的统一标准



### ip地址/InetAddress类

ipconfig 查看本机IP地址

127.0.0.1 回送地址, 一般用来测试

InetAddress类: 网络操作相关的类

方法:

InetAddress address=getByName( ) 传入主机名称或者IP地址 , 

返回一个IP地址给InetAddress对象 

address.getHostName( )  获取主机名

address.getHostAddress( ) 获取IP地址

### 端口

用两个字节表示的整数.取值范围0-65535 

0-1023用于一些知名的网络服务

端口号被占用会导致程序启动失败

### 协议

UDP: 不会确定对方是否存在. 

效率高,资源消耗小.  用于实时传输音频视频 等丢失一点都没什么关系的数据

TCP: 可靠无差错,必须确认服务端和客户端

三次握手:

1. 客户端发出请求,等待确认
2. 服务端回送一个响应,通知客户端已经收到了
3. 客户端再次发送确认信息,确认连接

### UDP发送/接收

两端各建立一个Socket对象,发送和接收数据

DatagramSocket类提供了基于UDP协议的Socket

​	**发送**

1. 创建DatagramSocket对象ds

2. 创建数据,打包

   DatagramPacket p= 

   new DatagramPacket ( 要发送的字节数组, 长度, InetAddress对象, 端口号)

3. 调用对象方法发送数据

   ds.send( dp );

4. 关闭发送端

   ds.close( );

​	**接收**

1. 创建用于接收的DatagramSocket 对象 

   DatagramSocket =new DatagramSocket ( **端口号** )  //接收时需要端口号

2. 创建一个用于接收的DatagramPacket

   DatagramPacket dp= new DatagramPacket( 字节数组, 长度 )  //长度可以是bys.length

3. 调用 ds.receive( dp )接收数据到dp中

4. 解析dp数据包 ,返回数据缓冲区:

   byte[] datas= dp.getData( )

5. String data= new String( bys, 0, bys.length )  转为字符串 

6. 记得close( )

### TCP发送/接收

通过IO流来进行通信

​	**发送**

1. Socket s = new Socket( 地址, 端口 )  ( 尝试建立连接,即等待ss.accept( ) )

2. s.getOutputStream( )  这个是该端口对应的输出流对象

   可以直接用: s.getOutputStream( ). write( )

   也可以保存为一个对象: OutputStream os= s.getOutputStream( )

3. 使用OutputStream的方法: flusk( ),write(),close()等等

​	**接收**

1. ServerSocket ss= new ServerSocket( 14838 );  //这个是服务端socket

2. Socket s = ss.accept( )  //发送端 s 连接到输出端 ss 

    accept实际上就是等待发送端创建连接,创建后返回一个连接完成的Socket对象

   所以实际上发送和接收都是Socker做到的,ServerSocker只负责搭建一个连接

   连接完就没ServerSocker啥事了

3. 创建byte数组bys

4. int len= **s**.getInputStream.read( byte[] )方法会读数据,存在bys中,方法返回实际长度.

5. String data= new String( bys, 0, len )  转为字符串

6. 记得close( )

### 几个特别关注的输入

键盘->server ( 持续输入,某值退出 )

```
BufferedReader reader=new BufferedReader(new InputStreamReader(System.in));
        String line;
        while((line=reader.readLine())!=null){
            if("不要停下来啊".equals(line)){
                break;
            }
        }
```

数据写入文本文件:

```
BufferedWriter writer=new BufferedWriter(new FileWriter(文件路径));
writer.write(line);
writer.newLine();
writer.flush(); //手动flush,防止一次没有填满缓存区
```

流写入文本文件:

```
BufferedWriter writer=
new BufferedWriter(new InputStreamReader(s.getInputStream()));
```

InputStreamReader 是字节流和字符流的桥梁

BufferedReader和BufferedWriter都需要字符流作为参数



shutdownOutput( )输出的结束标记

流传输完毕之后执行, 接收端



### 总结

Buffered 要传对应类型的流

BufferedWriter 传OutputStreamWriter(字节转字符) ,FileWriter 等字符流( read,write就是字符流 )

BufferedOutputStream 传其他的有input和output的,代表字节流



### lambda

其表达式整体作为一个接口的实例.

1. 可以用于实例化**函数式接口**(就是只有一个方法的接口)

   Interface Inter( ){ xxxx }

​		Inter inter = ( a ) -> a - 2    这时可以直接调用inter.方法

2. 类似其他语言,当做一个简短小巧的匿名函数
3. 一些函数的参数是一个接口.



一些例子:

**list. forEach**( item -> { } )  forEach这种赋一个函数进去的

**性能问题**

forEach是并行操作,大量数据时能提升CPU使用率,增强性能

少量数据时则会频繁切换流,导致性能降低



**官方定义的几个常用接口:**

* Function: 接收参数，并返回结果，主要方法 R apply(T t)    //函数类接口
  Consumer: 接收参数，无返回结果, 主要方法为 void accept(T t)  //消费者
  Supplier: 不接收参数，但返回结构，主要方法为 T get()    //生产者
  Predicate: 接收参数，返回boolean值，主要方法为 boolean test(T t)  //判断者

**引用对象(双冒号)**: 

对象::方法   如果是static方法还能 类名::方法

这一个整体是一个接口的实例.

所以可以直接定义一个接口,

Consumer consumer=Dog::eat( )   //Consumer是官方定义的一个函数式接口

一个更好的例子:

Consumer consumer=System.out::println   //这里就把println方法赋给了consumer



**与官方接口的结合**

比如这几个需求:

一个方法: 把一个int数据加上整数后转为字符串,输出

需要一个int,一个int转String的函数

convert( int i, Function< Integer,String > fun){

​		String s= fun.apply( i );

}

输入一个Integer, 返回一个String典型Function

此时用lambda:

convert( 3, i -> String. valueOf (i+2)  )

...( 更抽象了,现在连传入的参数都是抽象的规则 )



### 流:Stream

**Why**

流实际上就是另一种形式的数据,固定的Collection数据可以转换为stream.

把一段数据分成很多份,每份都有上一个部分的尾节点.

为什么要有这种形式呢?

1. 方便中间操作.在一个流的处理中时刻都是在遍历,所以可以轻松完成一些过滤,合并等操作
2. 充分发挥性能.因为可以传过来一点,就处理一点.



list.**stream**( ). **filter**( s->s.startsWith( "张" ) ).**filter**( s-> s.length( )==3 )

 .**forEach**( s ->sout( s ) )   首先.stream()将list变为流 ,然后filter()过滤 流



流的操作:

* 生成流

  Collection可以用stream( )

  Map体系的要间接生成: 

  用keySet( )生成键的流,values( )生成值的流,

   entrySet生成Stream  :Stream< Map.Entry< String,Integer > >    s=map.entrySet().stream()

  

  也可以用

  Stream.of( Collection ) 

  Stream.of( 3,4,6,7,9 ) 等方法返回对应泛型的Stream对象

  stream返回的是一个Stream对象,可以像这样接住Stream< String > s1=list.stream( )

​		

* 过滤流 

  filter( )上面讲了

  limit( 3 )  取前3个元素 

  skip( 3 )  跳过前3个元素 ( 两个叠加使用可以取中间部分 )

  split( "")  以什么为分隔

  

  concat( Stream1,Stream2 ) 合并两个流为一个

  distinct( Stream )   返回该流的不同元素

  sorted( )  返回该流自然排序的结果  //里面写一个Predicate表达式可以调整排序规则

  map( )  传一个Function表达式进去,出来的流是每个元素进行一次表达式运算的结果

  mapToInt( )   返回的是IntStream  该类有一个方法sum( )可以求和( 是map没有的 )

* 最终处理流  (没有返回值)

  forEach( Consumer )

  long  count() 流的元素数

  

  收集到Collection中:

  stream.collect( Collectors.xxx ) 该函数需要一个接口

  Collectors提供很多收集操作的接口

  比如toSet, toList,toMap等

  这些方法都可以传一个lambda进去,

  toMap需要传入两个流, 分别作键和值

  

  返回对应的集合对象

  ### 类加载

  ![image-20230113130236037](C:\Users\zh148\AppData\Roaming\Typora\typora-user-images\image-20230113130236037.png)

### 反射

JAVA反射机制是在运行状态中，对于**任意一个类**，都能够知道**这个类的所有属性和方法**；对于**任意一个对象**，都能够**调用它的任意一个方法和属性**；这种动态获取的信息以及动态调用对象的方法的功能称为java语言的反射机制。



**获取Class类的字节码对象:**

* 类名.class
* 对象.getClass()
* Class.forName( " " )内填某个类的全路径,即完整包名路径



**获取构造方法的方法:**

![image-20230113140543193](C:\Users\zh148\AppData\Roaming\Typora\typora-user-images\image-20230113140543193.png)

Constructor<?>[] cons= c.getConstructors( ) 这样,cons中就是c的所有**公共构造方法**对象

Constructor<?>[] cons= c.getDeclaredConstructors( )  这样可以获取包括**私有**的构造方法

Constructor<?>[] cons= c.getConstructor( String.class ,Integer.class )获取指定参数的构造方法 

获取了构造方法后就可以通过newInstance来创建类.

( 相当于把new给拆分成: 先通过上上面的那三个方法来获得class的字节码对象,然后通过上面的方法获得构造方法,最后newInstance )



**暴力反射**

和getDeclaredConstructor搭配使用.

通过getDeclaredConstructor获得的私有构造函数通常不能直接使用.

但是可以 con.setAccessible( ture )这样就能使用私有构造函数



**获取成员变量Fields**

Field类提供有关类或接口的单个字段的信息和动态访问

Class< ? > c = Class.forName( "xxx.Student" )  //现在c是Student类的字节码

Field[ ]  fields = c.getFields( )   //获取类c的**公共**成员变量数组

Field[ ]  fields = c.getDeclaredFields( )  //获取类c的**所有**成员变量数组

Field  field = c.getField( "name" )     //通过成员变量名获取成员变量



如何使用?

以第三个为例,此时field是Field类的一个实例,field中包含了几个信息:

1. 这是c对应的类的field( 即Student的field )
2. 这个field是Student里面的name成员变量

field.set( obj, "张三" );  //给obj的成员变量name 赋了一个张三的值



**获取成员方法**

getMethod和getDeclaredMethod和getMethods和getDeclaredMethods

getMethods 会获取自己的公共方法以及从父类继承的所有方法( 所以会出现很多从Object继承的类似wait,toString等等方法 )

getDeclaredMethods 这个不会获取继承的,只会获取自己的所有方法( 包括private )

getMethod( 方法名, 参数1.class,参数2.class....) 获取指定方法,返回一个Method接口对象



调用成员方法:

在获取了一个Method对象m后,调用某对象obj的m方法:

m.invoke( obj , Object...args 这个是参数列表的意思 )

这样就能调obj的m方法



### 模块化

jdk1.9特性

在一个项目下建多个模块,通过配置文件达成互相调用

模块之间互相独立, 可以不同时加载出来

**配置文件**

在模块的src目录下新建一个module-info.java

```
module myModule1{  //本模块名称
	exports 对外暴露的包路径;
	
	requires Module2需要依赖的其他模块名称;
	
}
```



### 服务模块:

将服务接口定义在一个模块中( 这个接口模块就是这个包的出口,写这个包的人只需要实现这些接口的内容,外界也只需要require包, uses这些service, 然后用这些模块 )

**首先在服务接口包中创建需要的接口**  规划一下需要实现什么

```
// 这是m1模块下的p1包下的一个接口
Interface myService{
	void service()
}
```

**然后在impl文件夹中写接口的实现类**  这是真的写功能

```
//新建服务接口包(这里是myService)下的impl文件夹,里面是myService的实现类
public class c implements MyService{
	public void service(){
		sout("提供服务");
	}
}
```

**最后在配置文件中 provide 一下服务**  可以决定用哪个类provide

```
// 这是m1模块的module-info.java
module m1{
	exports m1;
	provide myService with c; //这里指定myService的实现类为c
}
```

**使用服务:在配置文件中声明一下要uses该服务,然后用ServiceLoader来加载服务**

```
//这是要使用服务的module-info.java
module m2{
	uses myService;
}
```

```
// 这是真正使用服务的地方
psvm(){
	//加载服务
	ServiceLoader<myService> myservices= 	ServiceLoader.load(myService.class); 
	//一定要传Class对象进去
	
	//使用服务
	for(myService my : myservices ){ //ServiceLoader是可迭代的
		my.service();
	}
}
```
