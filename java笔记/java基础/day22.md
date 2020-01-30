* 一、继承Thread的方式

  1.提供一个继承于Thread类的子类

  2.重写Thread类的run():将创建的线程要执行的操作，声明在run()中。

  3.实例化Thread子类

  4.调用子类对象的start() 

Thread类的常用方法的测试

 1.run():Thread的子类一定要重写的方法。将此分线程要执行的操作，声明在run()中

 2.start():要想启动一个分线程，就需要调用start():①启动线程②调用线程的run()

 3.currentThread():静态方法，获取当前的线程

 4.getName():获取当前线程的名字

 5.setName(String name)：设置当前线程的名字

 6.yield():当前线程调用此方法，释放CPU的执行权

 7.join():在线程a中调用线程b的join()方法:只用当线程b执行结束以后，线程a结束阻塞状态，继续执行。

 8.sleep(long millitimes):让当前的线程睡眠millitimes毫秒

 9.isAlive():判断当前线程是否存活 

10.线程的优先级：

​      MAX_PRIORITY：10

​      NORM_PRIORITY：5 ---默认优先级

​      MIN_PRIORITY：1

​     设置优先级：setPriority(int priority); 

​     获取优先级：getPriority()；

   设置优先级以后，对高优先级，使用优先调度的抢占式策略，抢占低优先级的执行。但是并不意味着高优    先级的线程一定先于低优先级的线程执行，而是从概率上来讲，概率更大而已。

 线程通信：wait() / notify() / notifyAll()  ---->java.lang.Object类中定义的方法



# 一：继承Thread的方式  

  1.提供一个继承Thread类的子类 

  2.重写Thread类run():将创建的线程要执行的操作,声明在run()中 

  3.实例化Thread子类

  4.调用子类对象的start()方法

# 创建多线程的方式二:

  1.创建一个实现Runnable接口的类

  2.实现Runnable的run()

  3.创建当前实现类的对象

  4.将此对象作为参数传递到Thread类的构造器中,创建Thread类的对象

  5.通过Thread类的对象调用其start()



对比继承Thread类和实现Runnable接口的方式

 1.联系:public class Thread implements Runnable

 2.相同点:启动线程,使用的是同一个start()方法

 3.对比:实现Runnable接口要好一些. 

​    原因：①不影响类的继承,因为类是单继承的   

​               ②针对于有共享数据的操作,更适合使用Runnable的方式 ,换句话说,实现Runnable接口的方式,

​                   实现了代码和数据的分离

 4.面试题:创建多线程有几种方法?     继承Thread类,实现Runnable接口,实现Callable接口,使用线程池



模仿车站买票程序。开启3个窗口卖票。总票数为100张。-----使用实现的方式

  1.问题：出现了重票和错票

  2.问题出现的原因：一个窗口在没有售完票的情况下，其他的窗口参与进来，操作ticket，导致ticket输出的错误。

  3.解决的方案：当某一个窗口完全操作完ticket以后，其他窗口应该才被允许进来，继续操作ticket。

  4.java如何实现的？同步机制：①同步代码块    ②同步方法 

​       4.1 同步代码块：

​             synchronized(同步监视器){

​                   //需要被同步的代码

​           }

​          说明：需要被同步的代码：即为操作共享数据的代码

​          共享数据：多个线程共同操作的数据。比如：ticket

​          同步监视器：俗称：锁。 可以由任何一个类的对象充当。 要求：保证多个线程共用同一把锁！

​     4.2 同步方法：将操作共享数据的方法，声明为同步的。此方法即为同步方法。

​           使用同步方法解决实现方式的线程安全问题。

​           1.默认的同步方法（非静态的）的锁是：当前对象，也就是this.

​           2.默认的同步方法（静态的）的锁是：当前类本身.

​           使用同步方法解决继承方式的线程安全问题：

​             注意：继承的方式中，要慎用同步方法。

5. 好处：线程的同步机制，解决了线程的安全问题。

6. 劣势：在操作共享数据过程中，是单线程的。

   

 模仿车站买票程序。开启3个窗口卖票。总票数为100张     -----使用实现的方式

​     解决线程安全问题的方式三：ReentrantLock

​           存在线程的安全问题，使用Lock的方式解决线程安全问题。

 面试题：同步的方式和Lock的方式，解决线程安全方面的异同？

​     同：解决了线程安全问题

​     异：同步的方式：同步监视器在线程执行完操作共享数据的代码以后，自动释放

​            Lock的方式：需要显式的调用unlock()方法之后，才能保证其他线程操作共享数据。 

死锁：不同的线程分别占用对方需要的同步资源不放弃，都在等待对方放弃自己需要的同步资源，就形成了线程的死锁，是我们开发中需要规避的！





线程的通信：

   wait():一个线程在执行过程中，一旦调用此方法，则此线程进入阻塞状态，等待其他线程来唤醒自己。

   notify():一个线程在执行过程中，一旦调用此方法，则会唤醒被wait()的一个线程。高优先级的要优先被唤醒。

   notifyAll():一个线程在执行过程中，一旦调用此方法，则会唤醒所有被wait()的线程。

  例题：使用两个线程打印 1-100. 线程1, 线程2 交替打印

​       注意点：1.此三个方法必须使用在同步中。

​                      2.此三个方法的调用者是同步监视器！否则，如果三个方法的调用者不是同步监视器，报异常。

​                      3.此三个方法定义在Object类

​        面试题：sleep() 和  wait() 的异同？

​             1.方法声明在哪？ Thread:sleep()   Object:wait()

​             2.共同点：使得当前线程进入阻塞状态

​             3.使用的范围要求：sleep()使用没有情境的要求；wait()必须使用在同步代码块或同步方法中

​             4.都使用在同步当中的话：wait()需要唤醒：notify()/notifyAll();  sleep():不会释放锁；wait()会释放锁 



 String:字符串

​    1.字符串声明的数据，会存储在字符串常量池中。第一次声明时，需要创建相应的字符串。之后，如果声明的变量，其值与之前存在的字符串内容相同，则直接引用现成的字符串。

​    2.面试题：String s3 = new String("javaEE");创建的对象，在内存中生成了几个对象？

String:代表着不可变的字符序列。

  1.String类的声明public final class String implements java.io.Serializable, Comparable<String>, CharSequence

​      ①String声明为final，不可被继承。

​      ②实现Serializable：表明String可序列化。浏览器/客户端<--->服务器端     进程1<---->进程2    "{name=Tom,age=12}"    JSON:本质就是String

​      ③String重写了hashCode()/equals():常常将Map的key声明为String型。

​      ④实现Comparable接口：String可以比较大小。

​      ⑤实现CharSequence接口：String的底层声明了char[] value数组。

  2.如何理解String的不可变性：

​        ①向现有的字符串后添加新的字符串，必须声明新的字符串空间

​        ②将现有的字符串替换为新的字符串，必须声明新的字符串空间

​        ③只替换现有字符串中的指定某个字符，也必须声明新的字符串空间





String类与其它结构的转换：    

​     1.String 与包装类、基本数据类型变量间的转换    

​           String-->包装类、基本数据类型:调用包装类Xxx的parseXxx(String s)方法        

​                 String s = "123";     

​                         包装类、基本数据类型 -->String:调用String的valueOf(xxx xxx);    

​    2.String 与 字节数组间的转换   

​         String --> 字节数组:调用String类的getBytes()     

​         字节数组-->String:new String(byte[] buffer,startIndex,length)    

​    3.String 与 字符数组间的转换    
​         String --> 字符数组：调用String类的toCharArray()    

​         字符数组 -->String:new String(char[] cbuf,startIndex,length)    

​         public String substring(int startpoint):返回当前字符串中从startPoint位置开始，到末尾的子字符串。  

​         public String substring(int start,int end):返回当前字符串中从startPoint位置开始，到end结束的左闭右开区间的子字符串。

​         pubic String replace(char oldChar,char newChar):将字符串中指定的所有oldChar替换为newChar.

​         public String replaceAll(String old,String new):将字符串中指定的所有old替换为new.

​         public String trim():去除字符串首尾的空格

​         public String concat(String str):连接两个字符串

​         public boolean contains(CharSequence s)：判断当前字符串中是否包含s.

​         public String[] split(String regex)根据给定正则表达式的匹配拆分此字符串。



public int length():返回当前字符串的长度

public char charAt(int index)：获取指定索引位置的字符

public boolean equals(Object anObject)：比较两个字符串内容是否相等。

public int compareTo(String anotherString):比较两个字符串的大小

public int indexOf(String s):返回s在当前字符串中首次出现的位置。如果不存在，返回-1.

public int indexOf(String s ,int startpoint):

public int lastIndexOf(String s):返回s在当前字符串中末次出现的位置。如果不存在，返回-1.

public int lastIndexOf(String s ,int startpoint):

public boolean startsWith(String prefix)：判断当前的字符串是否以指定的prefix字符串开始的

public boolean endsWith(String suffix)：判断当前的字符串是否以指定的suffix字符串结束的

public boolean regionMatches(int firstStart,String other,int otherStart ,int length)   ？



面试题：

  String:不可变的字符序列；底层使用char[]存储

  StringBuffer:可变的字符序列；线程安全的，效率低；底层使用char[]存储  

  StringBuilder:可变的字符序列；线程不安全的，效率高，(jdk 5.0新增)；底层使用char[]存储

  类比：String --->数组； StringBuffer --->Vector   StringBuilder --->ArrayList

​            ArrayList list = new ArrayList();

​            list.add(123);//new Object[10];

​              ....

​              扩容:1.5倍的方式扩容。

​            这里：

​            String str = new String();//new char[0];

​            str.length();

​            String str1 = new String("abc");//new char[]{'a','b','c'};

​            对比：

​                StringBuffer s1 = new StringBuffer();//char[] value = new char[16]

​               StringBuffer s2 = new StringBuffer(10);//char[] value = new char[10]

​               s1.append("abc");//value[0] = 'a',value[1] = 'b',value[2] = 'c';

​               ...   每次添加时，都需要判断底层的char[]是否能够盛装下新要添加的字符串。

​                    如果不能盛装下，需要扩容。默认扩容为原来的2倍 + 2.   

​            启示：StringBuffer s1 = new StringBuffer(int capacity);开发中建议使用此构造器。

   

StringBuffer中的方法：

​     StringBuffer append(String s),

​     StringBuffer append(int n) ,

​     StringBuffer append(Object o) ,

​     StringBuffer append(char n)，

​     StringBuffer append(long n),

​    StringBuffer append(boolean n),

​    StringBuffer insert(int index, String str)

​    public StringBuffer reverse()

​    StringBuffer delete(int startIndex, int endIndex):删除当前可变字符串中从startIndex到endIndex结束的左闭右开区间的数据。

​    public char charAt(int n )

   public void setCharAt(int n ,char ch)

   StringBuffer replace( int startIndex ,int endIndex, String str)

   public int indexOf(String str)

   public String substring(int start,int end)

  public int length()

  总结：

​      增：append(Xxx xxx)

​      删：delete(int startIndex, int endIndex)

​      改：setCharAt(int n ,char ch) / replace( int startIndex ,int endIndex, String str)

​      查：charAt(int n)

​      插：insert(int index, String str)

​     长度：length()

​     遍历：使用for + charAt()