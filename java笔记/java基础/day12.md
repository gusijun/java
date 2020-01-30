equals 方法的使用

​     1.java.lang.Object 类中的equals()方法的定义:

​               public boolean equals(Object obj){  

​                           return(this == obj);

​             }  

​       说明:Object 类中equals()比较两个对象的引用地址是否相同，（或:比较两个引用是否指向同一个对象实体）

  2.像String,Date,File,包装类重写了Object类的方法，比较两个对象中的实体内容是否相等

  3.对于自定义类来讲,如果没有重写Object类中equals（）方法，仍然比较两个对象的引用地址是否相同

  4.一般情况下，在开发中一旦调用了自定义了的equals()，通常是重写以后的equals()方法

  5.重写equals()方法的规则:比较两个对象的属性是否都相等



 面试题: == 和 equals() 区别 ?

​              == :使用范围:可以操作基本数据类型 和 引用数据类型

​                    如果操作的是基本数据类型:比较两个基本数据类型变量的值是否相等

​                    如果操作的是引用数据类型:比较两个引用的地址是否相同

​             equals:使用范围:只适用于引用数据类型

​                        具体的使用:见上面的1-5





toString()的使用:

​        1.java.lang.Object 类中toString()定义如下: 

​             public String toString(){  

​                     return getClass().getName()+"@"+Integer.toHexString(hashCode());  

​             }

​       2.当我们打印一个对象的引用时，实际上就是调用了toString方法 

​       3.像String,Date,File,包装类等重写了Object类中的toString方法，返回其代表的具体内容

​       4.对于自定义类而言，如果我们没有重写object类中toString方法，则返回的仍然是地址值

​           如果重写了的话，重写规则:返回当前对象的属性信息