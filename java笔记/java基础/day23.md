jdk 8 之前 日期+时间 API的使用

java.util.Date类

​     |----java.sql.Date类

1.java.util.Date类：

​        如何实例化：两个构造器

​        常用方法：toString() / getTime();

 2.java.sql.Date类：与数据表中的Date类型的变量对应。    



构造器一：获取系统当前时间对应的Date对象

Date date = new Date();

getTime()：返回当前日期对应的毫秒数：当前时间与1970-1-1 00：00：00直接的毫秒数

构造器二：获取毫秒数所对应的Date对象

Date date1 = new Date(1502768492941L);



SQl:

java.sql.Date date2 = new java.sql.Date(1502768492941L);



SimpleDateFormat

使用默认构造器:SimpleDateFormat sdf = new SimpleDateFormat();

格式化：String format(Date date):

  Date date = new Date();

  String dateStr = sdf.format(date);



解析： Date parse(String dateStr)

Date date1 = sdf.parse("17-8-15 下午2:18");

System.out.println(date1);



java.text.SimpleDateFormat类

   1.SimpleDateFormat的作用：

​        格式化：日期--->文本

​        解析：格式化的逆过程，文本 --->日期

   2.SimpleDateFormat实例化

使用带参数的构造器

   SimpleDateFormat sdf1 = new SimpleDateFormat("EEE, d MMM yyyy HH:mm:ss Z");   

   SimpleDateFormat sdf1 = new SimpleDateFormat("yyyy-MM-dd hh:mm:ss");

格式化：

   String dateStr1 = sdf1.format(date);

   System.out.println(dateStr1);//2017-08-15 02:24:40

解析

​    Date date2 = sdf1.parse("2017-08-15 02:24:40");

​    System.out.println(date2);



java.util.Calendar(日历)类的使用

​    1.实例化Calendar calendar = Calendar.getInstance();

​     2.get()

​        int day = calendar.get(Calendar.DAY_OF_MONTH);

​        System.out.println(day);

​     3.set()

​        calendar.set(Calendar.DAY_OF_MONTH, 20);

​        day =   calendar.get(Calendar.DAY_OF_MONTH);

​        System.out.println(day);

​     4.add()

​         calendar.add(Calendar.DAY_OF_MONTH, -2);

​         day = calendar.get(Calendar.DAY_OF_MONTH);

​         System.out.println(day);

日历 --->日期

 Date date = calendar.getTime();

 System.out.println(date);

使用指定的Date对象，来设置calendar

​    Date date1 = new Date();

​    calendar.setTime(date1);

​    day = calendar.get(Calendar.DAY_OF_MONTH);

​     System.out.println(day);



LocalDate / LocalTime / LocalDateTime     -----重要//理解为对Calendar

```java
//实例化
//now()
LocalDate localDate = LocalDate.now();
LocalTime localTime = LocalTime.now();
LocalDateTime localDateTime =   LocalDateTime.now();

System.out.println(localDate);
System.out.println(localTime);
System.out.println(localDateTime);

//of()
LocalDate localDate2 = LocalDate.of(2017,8,15); 
System.out.println(localDate2);
LocalDateTime localDateTime2 = LocalDateTime.of(2017, 8, 15, 11, 11,23); System.out.println(localDateTime2);
System.out.println();
//getXxx():
System.out.println(localDateTime.getDayOfYear());
System.out.println(localDateTime.getDayOfMonth());
System.out.println(localDateTime.getDayOfWeek());
System.out.println(localDateTime.getMonth());
System.out.println(localDateTime.getMonthValue());
System.out.println(localDateTime.getHour());
System.out.println(localDateTime.getMinute());
//withXxx():体现了不可变性
LocalDateTime localDateTime3=localDateTime.withDayOfMonth(20); System.out.println(localDateTime);
System.out.println(localDateTime3);
LocalDateTime localDateTime4=localDateTime.withHour(12); System.out.println(localDateTime4);
//plus()//minus()
LocalDateTime localDateTime5 =localDateTime.plusDays(3); System.out.println(localDateTime5);
LocalDateTime localDateTime6 =localDateTime.minusMinutes(20); 
System.out.println(localDateTime6);
boolean isBefore =localDateTime.isBefore(localDateTime6); 
 System.out.println(isBefore);//false
boolean isAfter =localDateTime.isAfter(localDateTime6); System.out.println(isAfter);//true
//isLeapYear():
System.out.println(localDate.isLeapYear());
LocalDate localDate3 =localDate.minusYears(1); 
System.out.println(localDate3.isLeapYear());
```





Optional类使用的测试

   Optional:是一个封装了具体类型数据的容器。

​    其中，具体的类型：通过Optional的泛型体现。

​    具体类型的数据：通过Optional内部的T value体现



返回一个没有封装任何数据的Optional对象

​    Optional<Object> op = Optional.empty();

Optional<String> op1 = Optional.ofNullable("beijing");

isPresent():判断内部的数据是否存在

get():返回Optional对象内部封装的数据

of(T t):当t为null时，报异常。建议不用此方法

orElse(T t):如果调用对象包含值，返回该值，否则返回t



Integer类作为int的包装类，能存储的最大整型值为2^31−1， 

BigInteger类的数值范围较Integer类、Long类的数值范围要大得多，可以支持任意精度的整数。

在商业计算中，要求数字精度比较高，故用到java.math.BigDecimal类。

BigDecimal类支持任何精度的定点数。