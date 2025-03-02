# 5、快速排序（Quick Sort）

**算法描述：**

使用分治法来把一个串（list）分为两个子串（sub-lists）。具体算法描述如下：



● 从数列中挑出一个元素，称为“基准”（pivot）；



● 重新排序数列，所有元素比基准值小的摆放在基准前面，所有元素比基准值大的摆在基准的后面（相同的数可以到任一边）。在这个分区退出之后，该基准就处于数列的中间位置。这个称为分区（partition）操作；

● 递归地（recursive）把小于基准值元素的子数列和大于基准值元素的子数列排序。

  
![1714553214033-661d669b-8b7c-4f86-8a37-dc630acc1ab2.png](./img/9zM0TmT3ZqRqyiVq/1714553214033-661d669b-8b7c-4f86-8a37-dc630acc1ab2-590363.png)

<font style="color:rgb(32,36,41);">key</font><font style="color:rgb(32,36,41);"> </font><font style="color:rgb(32,36,41);">值的选取可以有多种形式，例如中间数或者随机数，分别会对算法的复杂度产生不</font><font style="color:rgb(32,36,41);">同的影响。</font>

**<font style="color:rgb(32,36,41);">代码实现：</font>**

```plain
import java.util.Arrays;
public class QuickSort {
    public static void main(String[] args) {
        int[] a = {2, 4, 6, 1, 3, 7, 9, 8, 5};
        quickSort(a, 0, a.length - 1);
        System.out.println(Arrays.toString(a));
    }

    //时间复杂度O(n*logn)，空间复杂度O(n*logn)
    public static void quickSort(int[] arr, int startIndex, int endIndex) {
        if (startIndex < endIndex) {
            //找出基准
            int partition = partition(arr, startIndex, endIndex);
            //分成两边递归进行
            quickSort(arr, startIndex, partition - 1);
            quickSort(arr, partition + 1, endIndex);
        }
    }

    //找基准
    private static int partition(int[] arr, int startIndex, int endIndex) {
        int pivot = arr[startIndex];
        int left = startIndex;
        int right = endIndex;
        while (left != right) {
            while (left < right && arr[right] > pivot) {
                right--;
            }
            while (left < right && arr[left] <= pivot) {
                left++;
            }
            //找到left比基准大，right比基准小，进行交换
            if (left < right) {
                swap(arr, left, right);
            }
        }
        //第一轮完成，让left和right重合的位置和基准交换，返回基准的位置
        swap(arr, startIndex, left);
        return left;
    }

    //两数交换
    public static void swap(int[] arr, int i, int j) {
        int temp = arr[i];
        arr[i] = arr[j];
        arr[j] = temp;
    }
}
```



> 更新: 2024-05-01 16:48:35  
> 原文: <https://www.yuque.com/zhichangzhishiku/edrbqg/kacwcitolf6rbetm>