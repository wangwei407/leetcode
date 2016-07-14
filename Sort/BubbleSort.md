# Bubble Sort
## 基本思路
从头开始 swap两个元素 每次遍历一遍数组后 最大的元素排在最后 所以每次遍历后 N=N-1
```java
   public static void bSort0(int []array){
        for (int i = 0; i < array.length; i++) {
            for (int j=1; j<array.length-i; j++){
                if(array[j-1]>array[j]){
                    swap(array,j-1,j);
                }
            }
        }
    }
```
## 优化一：设置一个flag 如果一趟发生了swap 那么则为true 否则false 如果有一趟完成了交换排序 那么久不会发生交换 
```java
  public static void bSort1(int [] array){
        boolean flag=true;
        int k=array.length;
        while (flag){
            flag=false;
            for(int j=1;j<k;j++){
                if (array[j-1] > array[j]) {
                    swap(array,j-1,j);
                    flag=true;
                }
            }
            k--;
        }
    }
  ```
  ## 优化二：如果数组的仅仅是前面部分无序 不再需要对后面的数进行排序 设置一个flag 来找出最后交换的位置
  ```java
      public static void bSort2(int [] array){
        int flag=array.length;
        int k;
        while(flag > 0){
            k=flag;
            flag=0;
            for(int j=1; j<k; j++){
                if(array[j-1] > array[j]){
                    flag=j;
                    swap(array,j-1,j);
                }
            }
        }
    }
    ```
    
