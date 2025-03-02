# 4、冒泡排序（Bubble Sort）

算法描述：  
● 比较相邻的元素。如果第一个比第二个大，就交换它们两个；  
● 对每一对相邻元素作同样的工作，从开始第一对到结尾的最后一对，这样在最  
后的元素应该会是最大的数；  
● 针对所有的元素重复以上的步骤，除了最后一个；  
● 重复步骤 1~3，直到排序完成。  
如果两个元素相等，不会再交换位置，所以冒泡排序是一种稳定排序算法。  
代码实现：  
package com.atguigu.interview.chapter02;  
/**  
Java  
*/  
Java  
publc class BubbleSort {  
Java  
/**  
Java

+ [@param](/param ) data 被排序的数组
Java  
*/  
Java  
public static void bubbleSort( int [] data) {  
Java  
int arrayLength = data.length;  
Java  
for ( int i = 1 ; i < arrayLength; i++) { //第 i 次排序  
Java  
for ( int j = 0 ; j < arrayLength - i; j++) { //从索引为 j 的数开始  
Java  
if (data[j] > data[j + 1 ]) { //相邻元素两两对比  
Java  
int temp = data[j + 1 ]; // 元素交换  
Java  
data[j + 1 ] = data[j];  
Java  
data[j] = temp;  
Java  
}  
Java  
}  
Java  
System.out.println( "第" + i + "次排序：  
\n" + java.util.Arrays.toString(data));  
Java  
}  
Java  
}  
Java  
public static void main(String[] args) {  
Java  
int  
[] data = { 3 , 44 , 38 , 5 , 47 , 15 , 36 , 26 , 27 , 2 , 46 , 4 , 19 , 50 , 4  
8 };  
Java  
System.out.println( "排序之前：\n" + java.util.Arrays.toString(data));  
Java  
bubbleSort(data);  
Java  
System.out.println( "排序之后：\n" + java.util.Arrays.toString(data));  
Java  
}  
Java  
}  
J

> 更新: 2024-05-01 16:46:34  
