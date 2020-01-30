  一、流的分类

   1.流的流向：输入流、输出流

   2.流中数据单位：字节流、字符流

   3.流的角色不同：节点流、处理流

  二、 抽象基类                          节点流(或文件流)                                       缓冲流(处理流的一种)：提高数据读写效率

​          InputStream                   FileInputStream(read(byte[]))                 BufferedInputStream(read(byte[])

​          OutputStream               FileOutputStream(write(byte[],0,len))  BufferedOutputStream(write(byte[],0,len)

​         Readed                            FileReader(read(char[]))                          BufferedReader(read(char[]) / readLine())

​         Writer                              FileWriter(write(char[],0,len))                  BufferedWriter(write(char[],0,len)





从指定文件中读取数据到控制台上

   1.要去读的文件一定要存在的,否则报FileNotFoundException

   2.因为需要保证流的资源关闭,所以异常的处理需要使用try-catch-finally



字节流：

 输入流:FileInputStream

  1.创建一个文件,指明读取数据的来源

  2.将file对象作为参数传递到流的构造器中,创建一个字节的输入流:FileInputStream

  3.read():读取文件中的下一个字节。如果到达文件末尾的话,返回-1

  4.关闭资源



 输出流:FileOutputStream

  1.造文件

  2.造流:输出流

  3.写出数据  getBytes()  字符串--->字节数组

  4.关闭资源

​     &gt;如果输出的文件不存在,则在输出执行的过程中,自动创建此文件

​     &gt;如果输出的文件存在：如果使用构造器：FileOutputStream(file)是对已存在的文件的覆盖, 

​                                              如果使用构造器:FileOutputStream(file,true)是在已有文件内容的基础上,继续写入内容



字符流：

​    FileReader 和 FileWriter的使用：只能用来处理文本文件的。

​    FileInputStream 和  FileOutputStream:适合用来处理非文本文件：.avi , .mp3, .jpg, .doc



   1.造文件

   2.造流：字符的输入流、字符的输出流

   3.读取数据并写出

   4.关闭资源



缓冲流的使用。

  1.缓冲流是处理流的一种

  2.作用：提高数据的读写效率

  3.类：  处理非文本文件：

​               BufferedInputStream

​               BufferedOutputStream

​              处理文本文件：

​              BufferedReader

​              BufferedWriter  --->readLine 读取一行

​                                           --->newLine 开始新的一行



理流之二：转换流

  1.转化流的作用：能够实现字节流与字符流之间的转换

  2.涉及到的流：

​       InputStreamReader:实现字节的输入流转换为字符的输入流

​       OutputStreamWriter:实现字符的输出流转换为字节的输出流

   编码的过程：字符串、字符数组--->字节数组

   解码的过程：字节数组---->字符串、字符数组

 3.常见的编码集：

​    ASCII：美国标准信息交换码，用一个字节的7位可以表示。

​    ISO8859-1：拉丁码表。欧洲码表.  用一个字节的8位表示。

​    GB2312：中国的中文编码表。

​    GBK：中国的中文编码表升级，融合了更多的中文文字符号。

​     Unicode：国际标准码，融合了多种文字。 所有文字都用两个字节来表示,Java语言使用的就是unicode

​     UTF-8：最多用三个字节来表示一个字符



处理流之三：标准的输入、输出流 

   System.in:标准的输入流，默认从键盘输入 

   *System.out:标准的输出流，默认从显示屏输出* 

   System.setIn():重新指定输入的位置 

   System.setOut():重新指定输出的位置



处理流之四：打印流 PrintStream 和 PrintWriter

处理流之五：数据流 DataInputStream 和 DataOutpuStream



处理流之六：对象流

  1.作用：用于存储和读取基本数据类型数据或对象的处理流。它的强大之处就是可以把Java中的对象写入到数据源中， 也能把对象从数据源中还原回来。

  2.涉及到的流：ObjectInputStream 和 ObjectOutputStream

  3.对象序列化机制：允许把内存中的Java对象转换成平台无关的二进制流，从而允许把这种二进制流持久地保存在磁盘上，或通过网络将这种二进制流传输到另一个网络节点。当其它程序获取了这种二进制流，就可以恢复成原来的Java对象.



提供一个自定义类，实现序列化机制。

   要求：1.自定义类实现Serializable接口

​               2.需要给当前的类声明全局的常量：serialVersionUID

​               3.要求类的属性也是可序列化的。 (默认情况下：String、基本数据类型都是可序列化的)

​             注意：不能序列化static和transient修饰的成员变量



RandomAccessFile的使用：随机存取文件流

   1.RandomAccessFile在java.io包下声明，直接继承于Object类

   2.既可以作为输入流，又可以作为输出流。

   3.如果输出到的文件不存在，则会在输出的过程中，自动创建此文件 。 如果输出到的文件存在，

​      则不是对文件的覆盖，而是对文件内容的覆盖。（默认从头覆盖）

   4.实现数据的“插入” 







