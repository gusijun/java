1.java中的容器--在内存层面,对数据进行统一的存储和管理:数组 ；java集合

​    扩展:数据的持久化:文件(.jpg;mp3); xml ; 数据库

2.数组在内存存储方面的特点:①数组初始化以后,长度就确定了                

​                                                   ②数组类型声明后，就决定了进行元素初始化的类型   

​                                              弊端:数组初始化以后,长度就不可变了     

​                                                       数组中提供的属性和方法很少,不便于进行添加,删除,插入等操作            

​                                                       数组存储的数据是有序的,可以重复的----->存储数据的特点单一    

​           String[] arr = new String[10]      

​          Object[]  

3.集合框架     

​     java.util.Collection:单列数据

​              |-------List子接口:存储有序的,可重复的数据---->“动态”数组

​                     |-----ArrayList:作为List的主要实现类,线程不安全的,效率高；底层使用数组

​                     |-----LinkedList:对于频繁的插入,删除操作，我们建议使用此类,效率高；底层使用双向链表实现        

​                     |-----Vector:List的古老实现类,线程安全的,效率低；底层使用数组实现

​     [面试题] ArrayList,LinkList,Vector区别?

​             共同点:ArrayList,LinkList,Vector都是List接口的实现类,存储的数据都是有序的,可重复的

​                          区别:如上

​                          List list = new ArrayList();

​                          list.add(..);

​                           ...

​                          一旦添加元素超出底层数组的长度,就需要扩容,默认扩容需要为原来的1.5倍，同时              

​                         需要将原有数组中的元素复制到新的数组中。

​        实际情况:需要存储80个数据到ArrayList中,建议:List list = new ArrayList(85);            

​             |-------Set子接口:存储无序的,不可重复的数据---->高中讲的“集合”

​                       |---- HashSet 主要实现类,底层实现:HashSet底层使用了HashMap  

​                       |---- LinkedHashSet 是HashSet的子类,可以按照添加的顺序实现遍历     

​                                (原因:在HashSet底层存储上的基础上,额外使用了一对指针,能够记录此Node元素的

​                                上一个元素和下一个元素) ---> 对于频繁的遍历，效率高

​                      |---- TreeSet : 可以按照添加元素的指定属性的大小实现遍历。底层实现：红黑树

​                                    TreeSet的使用

​                                   1.向TreeSet中添加的元素必须是同一个类创建的对象

​                                   2.TreeSet排序的方式:①自然排序<Comparable> ②定制排序

​                                   3.自然排序:  

​                                      ①要求添加的元素所在的类实现Compare接口 

​                                      ②重写接口中的CompareTo(Object obj)--->指明排序的规则      

​                                         如果此方法返回值0，则要新添加的元素添加不成功  

​                                      ③向TreeSet添加此实现类的对象即可

​                                   定制排序：

​                                       TreeSet的定制排序:     

​                                     1.提供Comparator接口匿名实现类的对象     

​                                     2.重写其中的compare(Object o1,Object o2),指明排序的规则     

​                                     3.将此实现类的对象作为参数传递到TreeSet的构造器中   

​                                     4.向TreeSet的对象中添加compare()方法中判断类的对象



​                    总结:   元素是否能add成功,是否能remove,是否contains..... 

​                                都依赖于compareTo或者compare方法   与元素所在类的hasCode/equals无关



set作为Collection的子接口,没有定义额外的方法set:存储无序的,不可重复的元素  

​       1.无序性！= 随机性.添加的元素,需要计算哈希值,此哈希值决定了在底层储存的位置,从存储位置上看,             

​                            是无序的   

​        2.不可重复性:保证set集合中不同对象使用对象所属类的equals()方法判断的话,一定返回false。

​        3.如何向Set中添加一个元素?哈希算法   

​               向Set中添加元素a,首先通过hasCode()，计算元素的哈希值,此哈希值就决定了此元素在Set底层

​               存储的位置，如果此存储位置上没有元素,则此元素a添加成功 ，如果此存储的位置上有元素b,则

​               调用元素a所在类的equals（）方法.将元素b作为参数传递过去,如果返回值为true，则表示元素

​               a和元素b相同，添加不成功，如果返回值为false,则认为元素a和元素b不相同,此时元素b可以添

​               加成功的.元素a和元素b使用链表存储（jdk7.0:a指向b；JDK8.0:b指向a）  

​      4.向Set中添加的元素,要求其所在的类要重写两个方法:       

​           equals() 和 hashCode() 

​      5.必须要求添加的元素所在的类中重写equals() 和 hashCode（）保持一致



Map:存储的是双列数据：key-value 

​     1.所有的key构成的是集合是set:无序的,不可重复的 

​     2.所有value构成的是集合Collection:无序的,可以重复的 

​     3.一个key-value构成一个Entry

​     4.所有的Entry构成的集合是Set:无序的,不可重复的  

 HashSet的底层使用HashMap存储的 

 HashMap的所有key构成的集合是HashSet



|----HashMap:Map的主要实现类,线程不安全,效率高；可以存储null的key和value 

​         (存储结构：Jdk7.0数组+链表,Jdk8.0数组+红黑树)   

​          |----LinkedHashMap:HashMap的子类,可以按照添加的顺序遍历,对于频繁的遍历效率高

​                   (在HashMap存储的基础上,使用了一对指针,来记录添加元素的顺序)

|----TreeMap：可以按照key的指定的属性进行排序,遍历,底层实现:红黑树

|----Hashtable：Map的古老实现类:线程安全,效率低;不可以存储null的key和value 

​            |----Properties:Hashtable的子类，常常用来处理属性文件，其key和value都是String类型的



Map常用方法：

  添加:put(Object key,Object value)

  修改:put(Object key,Object value)

  删除:Object remove(Object obj)

  长度:size()

  清空数据:clear()

  是否为空isEmpty()

​     1.遍历所有的key

​         Set keySet = map.keySet();

​          Iterator iterator = keySet.iterator();

​          while(iterator.hasNext()){ 

​                 System.out.println(iterator.next());

​        }

   

​     2.遍历所有的value

​          Collection coll = map.values();

​          for(Object obj:coll){  

​               System.out.println(obj);

​         }



​    3.遍历所有的key-value

​          1.方式一：

​           Set keySet1 = map.keySet();

​           for(Object key:keySet1){

​                  System.out.println(key+"---->"+map.get(key));

​         }

​         2.方式二：

​         Set entrySet = map.entrySet();

​          for(Object o:entrySet){ 

​                Map.Entry entry = (Map.Entry)o;

​                System.out.println(entry.getKey()+"********"+entry.getValue());

​          }   



Map常用方法：

  添加:put(Object key,Object value)

  修改:put(Object key,Object value)

  删除:Object remove(Object obj)

  长度:size()

  清空数据:clear()

  是否为空isEmpty()



 总结:

​      增：put(Object key,Object value)

​      删：Object remove(Object obj)

​      改：put(Object key,Object value)

​      查：get(Object key)

​      长度:size()

​      遍历:keySet() / values() / entrySet()List (index--->数据)/ Set（很少用）/ Map（key --> 数据）



   说明：1.向List中添加自定义类的对象的话,要求此定义类要重写equals()方法

​               2.补充:数据结构解决两个问题:

​                           1.数据之间逻辑关系：一对一，一对多，多对多...

​                           2.数据的存储结构:①顺序存储:一维数组 ②链式存储

 4.测试Collection中的常用方法

​       ①size（）返回集合中存储的元素的个数

​       ②add(Object obj) 将obj添加到当前的集合中

​       ③addAll(Collection coll) 将coll1集合中的所有元素添加到当前集合中

​       ④isEmpty() 判断当前集合是否为空

​       ⑤clear 清除当前集合

​       ⑥contains(Object obj) 判断当前集合中是否包含obj：调用了obj所在类的equals（）方法

​       ⑦containsAll(collection coll)    当前集合是否包含coll中的所有元素

​       ⑧remove(Object obj):从当前集合中移除obj元素.仍然需要obj所在类的equals的方法

​       ⑨removeAll(Collection coll):差集:从当前集合中移除coll集合中的元素

​       ⑩retainAll(Collection coll)：交集：获取当前集合和coll共有的元素

​       ⑪equals(Object obj):比较当前对象和obj是否相等。

​       ⑫hashCode():获取当前对象的哈希值

​       ⑬toArray()：将集合转换成数组:Object[]

​       ⑭toArrays(T[] arr):略

​       ⑮Iterator():集合元素的遍历。迭代器

​          hasNext():判断是否还有下一个元素

​          next():①指针下移 ②将指针下移以后集合位置上的元素返回



5.规定：如果集合中存储自定义类的对象，要求自定义重写equals方法

6.集合：很常用。

​     掌握点：层次一：选择合适的集合类实现数据的保存,调用其内部的相关方法

​                    层次二:不同的集合类底层的数据结构为何？如何实现数据的操作的：增删改查等。



 集合的遍历:

​     方式一：使用Iterator实现

​     方式二：增强for循环(foreach循环)

​                 for(集合元素的类型 局部变量 : 集合引用)



List:

在Collection的基础上，新增的方法：

​       void add(int index, Object ele):在index位置插入ele元素

​       boolean addAll(int index, Collection eles):从index位置开始将eles中的所有元素添加进来 

​      Object get(int index):获取指定index位置的元素

​      int indexOf(Object obj):返回obj在集合中首次出现的位置.如果不存在，返回-1.

​      int lastIndexOf(Object obj):返回obj在当前集合中末次出现的位置.如果不存在，返回-1.

​      Object remove(int index):移除指定index位置的元素，并返回此元素

​      Object set(int index, Object ele):设置指定index位置的元素为eleList

​      subList(int fromIndex, int toIndex):返回从fromIndex到toIndex位置的左闭右开区间的子集合    

​      substring(int from ,int to) /  read(int from,int length)  

​      总结：List中的常用方法： 

​           增：add(Object obj)

​           删：remove(Object obj) / remove(int index)  

​           改：set(int index, Object ele)

​           查：get(int index)

​           插：add(int index, Object ele)

​           遍历：iterator();增强for;for   

​           长度：size()