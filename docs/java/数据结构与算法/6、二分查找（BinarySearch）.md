# 6、二分查找（Binary Search）

**算法描述：**

● 二分查找也称折半查找，它是一种效率较高的查找方法，要求列表中的元素首先要进行有序排列。

● 首先，假设表中元素是按升序排列，将表中间位置记录的关键字与查找关键字比较，如果两者相等，则查找成功；

● 否则利用中间位置记录将表分成前、后两个子表，如果中间位置记录的关键字大于查找关键字，则进一步查找前一子表，否则进一步查找后一子表。

● 重复以上过程，直到找到满足条件的记录，使查找成功，或直到子表不存在为止，此时查找不成功。

**代码实现：**

```java
 /**
  * 使用递归的二分查找
  *title:recursionBinarySearch
  *@param arr 有序数组
  *@param key 待查找关键字
  *@return 找到的位置
  */
 public static int recursionBinarySearch(int[] arr,int key,int low,int high){
  
  if(key < arr[low] || key > arr[high] || low > high){
   return -1;    
  }
  
  int middle = (low + high) / 2;   //初始中间位置
  if(arr[middle] > key){
   //比关键字大则关键字在左区域
   return recursionBinarySearch(arr, key, low, middle - 1);
  }else if(arr[middle] < key){
   //比关键字小则关键字在右区域
   return recursionBinarySearch(arr, key, middle + 1, high);
  }else {
   return middle;
  } 
  
 }
```

> 更新: 2024-05-01 16:51:29  
