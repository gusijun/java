### 一、Lambda 表达式的基础语法 :java8中引入了新的操作符“->” 该操作符称为箭头操作符或Lambda操作符
​       **箭头操作符 Lambda 表达式拆分为两部分:**
 	  	左侧：Lambda 表达式的参数列表
 	  	右侧：Lambda 表达式所需执行的功能,即 Lambda 体



* 语法格式一:无参数,无返回值
        	 () -> System.out.println("Hello Lambda");
* 语法格式二:有一个参数,并且无返回值
       	  (x) -> System.out.println(x);
* 语法格式三:若只有一个参数,小括号可以省略不写
        	  x -> System.out.println(x);
* 语法格式四:有两个以上的参数,有返回值,并且Lambda体中有多条语句
          Comparator<Integer> com = (x,y) -> {
              System.out.println("函数式接口");
              return Integer.compare(x,y);
            };
* 语法格式五:若Lambda体中只有一条语句,return和大括号都可以省略不写
* 语法格式六:Lambda表达式的参数列表的数据类型可以省略不写,因为JVM编译器通过上下文推断出,数据类型,即“类型推断”
            (Integer x,Integer y) -> Integer.compare(x,y)；

上联:左右遇一括号略
下联:左侧推断类型省
横批:能省则省



### 二: Lambda 表达式需要“函数式接口”的支持

​         **函数式接口:接口中只有一个抽象方法的接口,称为函数式接口。可以使用@FunctionalInterface 修饰
​        			     可以检查是否是函数接口**


​	     **Java8内置的四大核心函数式接口**

​	    Consumer<T> : 消费型接口
​    	   		void accept(T t);

 	   Supplier<T> : 供给型接口
    		   	T get();	

 	   Function<T,R> : 函数型接口
    			   R apply(T t);

  	  Predicate<T> : 断言型接口
    			   boolean test(T t);

**一.方法引用:若Lambda体中的内容有方法已经实现了,我们可以使用"方法引用"
           (可以理解为方法引用是Lambda表达式的另一种体现)**

   主要有三种语法格式:

   对象::实例方法名

   类::静态方法名

   类::实例方法名

   注意:
       1).Lambda体中调用方法的参数列表与返回值类型,要与函数式接口中的抽象方法的函数列表和返回值类型保持一致！
       2).②若Lambda 的参数列表的第一个参数，是实例方法的调用者，第二个参数(或无参)是实例方法的参数  时，格式： ClassName::MethodName		   			



**二.构造器引用**
       格式:
       ClassName::New

   注意:需要调用的构造器的参数列表要与函数式接口中抽象方法的参数列表保持一致！(个数)

**三:数组引用:**
       Type::new