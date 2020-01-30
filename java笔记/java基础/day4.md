素数判断：

1.

```java
import java.util.Scanner;
public class f1{
    public static void main(String[] args){
        for(int i=2;i<=100000;i++){
            boolean isFlag = true;
            for(int j=2;j<i;j++){
                if(i%j==0){
                    isFlag=false;
                }
            }
            if(isFlag){
                System.out.println(i);
            }
        }
       
    }
}

```

这种方式浪费内存，外循环 boolean = true 相当于每次重新定义一个变量



2.

```java
import java.util.Scanner;
public class f1{
    public static void main(String[] args){
        boolean isFlag = true;
        for(int i=2;i<=100000;i++){
            for(int j=2;j<i;j++){
                if(i%j==0){
                    isFlag=false;
                }
            }
            if(isFlag){
                System.out.println(i);
            }
            isFlag = true;
        }
    }
}

```

这种方式多写一行代码



3.

```java
public class f1{
    public static void main(String[] args){
        long start = System.currentTimeMillis();
        int PrimeNumberCount = 0;
        for(int i=2;i<=100000;i++){
            boolean isFlag = true; //标识
            //优化2:针对于质素数的优化
            for(int j=2;j<=Math.sqrt(i);j++){
                if(i%j==0){
                    isFlag=false;
                    //优化1:主要针对于非质数
                    break;//  结束包裹break关键字最近的一层
                }
            }
            if(isFlag){
                PrimeNumberCount++;
            }
        }
        System.out.println(PrimeNumberCount);
        long end = System.currentTimeMillis();
        System.out.println("时间:"+(end-start));
    }
}

```



currentTimeMillis()     获取系统当前时间对应的毫秒数

break   结束包裹break关键字最近的一层



break 和 continue

适用范围：                                                           在循环中，表示：

break: switch-case 或者 循环结构                     结束当前循环

continue: 循环结构                                              结束当次循环

相同点：

关键字后面不能有输出语句，编译不通过

附加：带标签的break和continue的使用