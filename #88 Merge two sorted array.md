# Given two sorted integer arrays nums1 and nums2, merge nums2 into nums1 as one sorted array.
Note:
You may assume that nums1 has enough space (size that is greater or equal to m + n) to hold additional elements from nums2. The number of elements initialized in nums1 and nums2 are m and n respectively.
## 思路:首先考虑一下时间复杂度的问题 因为是两个排序好的数组 并且数组一的大小是两个数组的总大小 所以其他问题不用考虑 考虑的是时间上的最优解
* 因为容器是数组 用insert方法会使整个数组后移 所以时间复杂度是O(nm) 
* 考虑到数组是排序好的 所以直接从最后开始比较 把最大的放到最后就可以了
 * 在这种情况下 有两种情况 数组二先遍历完 那么我们完成了任务 直接结束退出
 * 如果数组二并没有遍历完 这意味着数组一已经用完 当前的newIdx就等于idx2 所以直接把数组二未遍历的元素插进去就可以了 时间复杂度是O(m+n) 空间复杂度是O(m+n)
**以后思考问题还是要先想想时间和空间复杂度的问题 在做算法** 
```python
class Solution(object):
    def merge(self, nums1, m, nums2, n):
        """
        :type nums1: List[int]
        :type m: int
        :type nums2: List[int]
        :type n: int
        :rtype: void Do not return anything, modify nums1 in-place instead.
        """
        newIdx=n+m-1
        idx1=m-1
        idx2=n-1
        while idx1>=0 and idx2>=0:
          if(nums2[idx2]>nums1[idx1]):
            nums1[newIdx]=nums2[idx2]
            idx2-=1
          else:
            nums1[newIdx]=nums1[idx1]
            idx1-=1
          newIdx-=1
        //another case: 数组一先遍历完了
        if(idx2>-1):
          for i in range(0,newIdx+1) #newIdx=idx2 in this situation
            nums1[i]=nums2[i]

```

```java
public class Solution {
    public void merge(int[] nums1, int m, int[] nums2, int n) {
        int idx=n+m-1,idx1=m-1,idx2=n-1;
        while(idx>=0){
            if(idx1<0 || (idx2>=0 && nums1[idx1]<nums2[idx2])) nums1[idx]=nums2[idx2--];
            else nums1[idx]=nums1[idx1--];
            idx--;
        }
    }
}
```
