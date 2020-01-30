一、Stream API 的操作步骤：

   1. 创建 Stream

   2. 中间操作

   3. 终止操作(终端操作)

      

中间操作:

 筛选与切片

​	filter——接收 Lambda ， 从流中排除某些元素。
​	limit——截断流，使其元素不超过给定数量。
​	skip(n) —— 跳过元素，返回一个扔掉了前 n 个元素的流。若流中元素不足 n 个，则	返回一个空流。与   limit(n) 互补
​	distinct——筛选，通过流所生成元素的 hashCode() 和 equals() 去除重复元素

映射
  map——接收 Lambda ， 将元素转换成其他形式或提取信息。接收一个函数作为参数，该函数会被应用到每     个元素上，并将其映射成一个新的元素。
 flatMap——接收一个函数作为参数，将流中的每个值都换成另一个流，然后把所有流连接成一个流

sorted()——自然排序
sorted(Comparator com)——定制排序



终止操作:
   allMatch——检查是否匹配所有元素
   anyMatch——检查是否至少匹配一个元素
   noneMatch——检查是否没有匹配的元素
   findFirst——返回第一个元素
   findAny——返回当前流中的任意元素
   count——返回流中元素的总个数
   max——返回流中最大值
   min——返回流中最小值

归约
reduce(T identity, BinaryOperator) / reduce(BinaryOperator) ——可以将流中元素反复结合起来，得到一个值。

收集

collect——将流转换为其他形式。接收一个 Collector接口的实现，用于给Stream中元素做汇总的方法

注意：流进行了终止操作后，不能再次使用



二、Optional 容器类：用于尽量避免空指针异常
*  Optional.of(T t) : 创建一个 Optional 实例
*  Optional.empty() : 创建一个空的 Optional 实例
*  Optional.ofNullable(T t):若 t 不为 null,创建 Optional 实例,否则创建空实例
*  isPresent() : 判断是否包含值
*  orElse(T t) :  如果调用对象包含值，返回该值，否则返回t
*  orElseGet(Supplier s) :如果调用对象包含值，返回该值，否则返回 s 获取的值
*  map(Function f): 如果有值对其处理，并返回处理后的Optional，否则返回 Optional.empty()
*  flatMap(Function mapper):与 map 类似，要求返回值必须是Optional



三、时间

1. LocalDate、LocalTime、LocalDateTime
2. Instant : 时间戳。 （使用 Unix 元年  1970年1月1日 00:00:00 所经历的毫秒值）
3. 
   Duration : 用于计算两个“时间”间隔
   Period : 用于计算两个“日期”间隔

4. TemporalAdjuster : 时间校正器
5. DateTimeFormatter : 解析和格式化日期或时间
6. ZonedDate、ZonedTime、ZonedDateTime ： 带时区的时间或日期

