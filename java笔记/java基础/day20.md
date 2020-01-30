1. jdk 7.0 时，引入了 Path、Paths、Files三个类。

2.  此三个类声明在：java.nio.file包下。

3.  Path可以看做是java.io.File类的升级版本。也可以表示文件或文件目录，与平台无关

4. 如何实例化Path:使用Paths. 

     static Path get(String first, String … more) : 用于将多个字符串串连成路径

     static Path get(URI uri): 返回指定uri对应的Path路径 

   

   ## Path:

   String toString() ： 返回调用 Path 对象的字符串表示形式

   boolean startsWith(String path) : 判断是否以 path 路径开始

   boolean endsWith(String path) : 判断是否以 path 路径结束

   boolean isAbsolute() : 判断是否是绝对路径

   Path getParent() ：返回Path对象包含整个路径，不包含 Path 对象指定的文件路径

   Path getRoot() ：返回调用 Path 对象的根路径

​       Path getFileName() : 返回与调用 Path 对象关联的文件名

​       int getNameCount() : 返回Path 根目录后面元素的数量(层数)

​       Path getName(int idx) : 返回指定索引位置 idx 的路径名称

​       Path toAbsolutePath() : 作为绝对路径返回调用 Path 对象

​       File toFile(): 将Path转化为File类的对象



## Files

Path copy(Path src, Path dest, CopyOption … how) : 文件的复制      

​    &gt;要想复制成功，要求path1对应的物理上的文件存在。path1对应的文件没有要求。

​      Files.copy(path1, path2, StandardCopyOption.REPLACE_EXISTING); 当已存在时做覆盖

Path createDirectory(Path path, FileAttribute<?> … attr) : 创建一个目录      

​      要想执行成功，要求path对应的物理上的文件目录不存在。一旦存在，抛出异常。

Path createFile(Path path, FileAttribute<?> … arr) : 创建一个文件      

​      要想执行成功，要求path对应的物理上的文件不存在。一旦存在，抛出异常。

void delete(Path path) : 删除一个文件/目录，如果不存在，执行报错

void deleteIfExists(Path path) : Path对应的文件/目录如果存在，执行删除.如果不存在，正常执行结束

Path move(Path src, Path dest, CopyOption…how) : 将 src 移动到 dest 位置      

   要想执行成功，src对应的物理上的文件需要存在，dest对应的文件没有要求。

   Files.move(path1, path2, StandardCopyOption.ATOMIC_MOVE);

long size(Path path) : 返回 path 指定文件的大小



boolean exists(Path path, LinkOption … opts) : 判断文件是否存在

boolean isDirectory(Path path, LinkOption … opts) : 判断是否是目录

boolean isRegularFile(Path path, LinkOption … opts) : 判断是否是文件

boolean isHidden(Path path) : 判断是否是隐藏文件

​    &gt;要求此path对应的物理上的文件需要存在。才可判断是否隐藏。否则，抛异常

boolean isReadable(Path path) : 判断文件是否可读

boolean isWritable(Path path) : 判断文件是否可写

boolean notExists(Path path, LinkOption … opts) : 判断文件是否不存在





StandardOpenOption.READ:表示对应的Channel是可读的。 

StandardOpenOption.WRITE：表示对应的Channel是可写的。

StandardOpenOption.CREATE：如果要写出的文件不存在，则创建。如果存在，忽略 StandardOpenOption.CREATE_NEW：如果要写出的文件不存在，则创建。如果存在，抛异常



SeekableByteChannel newByteChannel(Path path, OpenOption…how) : 获取与指定文件的连接，how 指定打开方式。

DirectoryStream<Path>  newDirectoryStream(Path path) : 打开 path 指定的目录

InputStream newInputStream(Path path, OpenOption…how):获取 InputStream 对象

OutputStream newOutputStream(Path path, OpenOption…how) : 获取 OutputStream 对象





jdk 7 提供基于try-catch的自动资源管理

能够实现资源的自动关闭，需要满足：

  1.可以在一条 try 语句中管理多个资源，每个资源以“;” 隔开即可。

  2.需要关闭的资源，必须实现了 AutoCloseable 接口或其子接口 Closeable

 目的：不需要再使用finally，显式的关闭资源了。

