```java
数组倒序

1. int[] arr =  new int[]{1,2,3,4,5};

for(int i=0,j=arr.length; i < j;i++,j--){
        int temp = arr[j]；
        arr[j] = arr[i];
        arr[i] = temp;
}

2.

for(int i=0;i<arr1.length/2;i++){ 
     int temp = arr[arr.length-1-i];   
     arr[arr.length-1-i] = arr[i];   
     arr[i] = temp;
     }


```

冒泡排序：

```java
import java.util.Scanner;
public class f2{
     public static void main(String[] args){ 
     // ToDo 冒泡排序   
     long start = System.currentTimeMillis();
     Scanner s = new Scanner(System.in);    
     int num;  
     System.out.println("请输入数组元素个数:");  
     num = s.nextInt(); 
     int[] arr = new int[num];
     System.out.println("请输入数组元素:");
     for(int i=0;i<arr.length;i++){  
           arr[i] = s.nextInt(); 
      }    
      // ToDo 前面所有的数都排序完后，最后一个数就不用判断了  
     for(int i=0;i<arr.length-1;i++){          
     //ToDo 由于下面if判断i+1，所以循环条件是j<arr.length-1，否则会报错    
     // ToDo 每次排序都会少一个数，所以是j<arr.length-1-i  
     for(int j=0;j<arr.length-1-i;j++){ 
            if(arr[j]>arr[j+1]){             
                 int temp = arr[j+1];      
                 arr[j+1] = arr[j];   
                 arr[j] = temp;   
                 }   
               } 
             }  
     System.out.println("排序后的元素为:");   
     for(int i=0;i<arr.length;i++){  
     System.out.print(arr[i]+"\t"); 、
     }   
     System.out.println();
     long end = System.currentTimeMillis();   
     System.out.println("程序运行时间:"+(end-start)); 
     }
  }
```

Arrays  数组工具类

equals 比较两个数组的元素是否完全相同

toString  输入显示数组的具体元素

fill  将数组所有元素重新赋值，赋值为参数2

sort  底层元素用的快速排序

binarySearch 二分法查找



数组常见异常：

数组下角标越界异常：

ArrayIndexOutOfBoundsException

空指针异常：

NullpointerException



