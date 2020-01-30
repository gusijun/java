异常的体系结构:    

​      java.lang.Throwable        

​       ----Error:错误。不编写针对代码进行处理             

​           -----StackOverflowError       

​           -----OOM   

​      ----Exception:异常:可以编写针对性的代码进行处理      

​            -----编译时异常:编译时就不通过的异常,报出来的异常  

​            -----运行时异常(RuntimeException):编译通过,运行时不通过,报出来的异常      

​                | -----NullPointerException:空指针异常                

​                |-----ArrayIndexOutOfBoundsException:数组角标越界异常  

​                |-----ClassCastException:类型转换异常        

​                |-----NumberFormatException:数值格式化异常       

​                |-----InputMismatchException:输入的类型不匹配       

​                |-----ArithmeticException:算术异常        

​                |----------。。。  

  面试题:常见的异常?并举例说明



如何处理异常(Exception)？ 

​    java提供了异常处理的:抓抛模型   

   1.过程一:“抛”:程序在正常的执行过程中,一旦出现异常，就会在相应的代码处生成相应的异常类的对象。

​                    并将对象抛出,异常出现位置后面的代码就不再执行。    

​                    &gt;异常出现位置的后面的代码不再执行   

​                    &gt; 异常对象产生的方式:①自动抛出 ②手动抛出(在方法内,使用throw + 异常类的对象)

​    2.过程二:“抓”:看出是异常的处理的方法:try catch finally;throws   

​        try{  

​             //可能出现异常的代码   }catch(Exception el){ 

​             //处理异常的方式1   }catch(Exception e2){   

​             //处理异常的方式2   }...   

​       finally{     //一定要被执行的操作   }  

​      说明:    

​          1.finally是可选的     

​          2.在执行try中的语句是时,一旦出现异常,就会抛出相应异常的对象       

​             此对象会在如下的catch中进行匹配,一旦匹配成功,就进入相应的

​             catch的代码块中进行相应的异常处理,一旦处理完成,就跳出整个   

​             try-catch结构，不再执行其后的catch语句。  

​          3.多个catch语句中的异常类型说明:子类异常必须声明在父类异常的上面, 

​              否则编译不通过。如果多个异常类型没有子父类关系,则没有顺序要求。     

​          4.执行完catch语句以后,如果其结构还有操作,则可以正常执行。    

​          5.在try中定义的变量,其作用于仅限于try声明的一对{},出了此{}，不可被调用 

​          6.catch中常见的异常处理方法:

​                    ①getMessage()返回一个String变量       

​                    ②printStackTrace();打印异常产生的堆栈信息     总结:运行时异常

​          7.try-catch-finally  结构可以嵌套



关于try-catch-finally结构中finally的使用:  

​       1.可选的   

​       2.即使在catch中出现异常,try中有return；catch中有return；三种情况,finally   

​          中的代码也一定会执行！   

​        3.开发中的应用:IO流资源,网络Socket，数据库连接等,JVM不会自动进行资源的关闭和垃圾的回收,    

​           需要我们手动去释放资源。所以此操作必须声明在finally中。



异常的的处理方式二:throws + 异常类型  

​        格式:在方法的声明后,使用 “throws + 异常类型 ”,表示:一旦方法执行过程中,出现异常    

​              ，将此异常的对象抛出。  

​        1.上述出现的异常对象，会抛给方法的调用者。比如method1()在method()2   

​            调用,如果method()1出现异常,则此异常抛给了method()2。  

​         2.体会try-catch-finally:真正处理异常,一旦处理完,就不会影响后续代码执行     

​            throws:并没有真正的处理异常。   

​          3.总结:开发中如何选择使用哪种方式处理?    

​                  3.1如果父类被重写的方法没有throws的方式处理异常,则子类重写的方法也不能用 throws的  方式去处理异常,只能用try-catch-finally。 

​                  3.2 在一个方法a中,调用了另外的3个方法,此3个方法通常是递进关系的。一般情况下,        

​                        此3个方法中如果出现异常,通常使用throws的方式处理异常。然后统一在方法a中         

​                        使用try-catch-finally进行处理。



规定:子类重写的方法抛出的异常类型不能大于父类被重写的方法抛出的异常



包装类Integer (parseInt) 将字符串转成整数



注解：代码里的特殊标记

、OVerride 重写

​    Deprecated 过时   

​    SuppressWarnings 抑制编译器警告



元注解：解释说明当前注解的

​    

