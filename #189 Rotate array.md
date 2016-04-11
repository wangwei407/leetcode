#Rotate an array of n elements to the right by k steps.

For example, with n = 7 and k = 3, the array [1,2,3,4,5,6,7] is rotated to [5,6,7,1,2,3,4].

Note:
Try to come up as many solutions as you can, there are at least 3 different ways to solve this problem.
## Method 1: run timeO(N) sapce O(N)
### find the new array start index: n-(k%n) then move the element
```python
class Solution(object):
    def rotate(self, nums, k):
        """
        :type nums: List[int]
        :type k: int
        :rtype: void Do not return anything, modify nums in-place instead.
        """
        n=len(nums)
        newStart=n-(k%n)
        nums[:]=nums[newStart:]+[newStart:]
```
## Method2: find the newStart index, use three times reverse. For example,[1,2,3,4,5] k=3 
* first, find the newStart index=n-k%n=2 
* reverse newStart:end [1,2,3,4,5] -> [1,2,5,4,3]
* reverse 0: newStart [1,2,5,4,3] -> [2,1,5,4,3]
* reverse 0: end [2,1,5,4,3] -> [3,4,5,1,2]
```java
public class Solution {
    public void rotate(int[] nums, int k) {
        int length=nums.length;
        int startIdx=length-k%length;
        reverse(nums,startIdx,length-1);
        reverse(nums,0,startIdx-1);
        reverse(nums,0,length-1);
    }
    private void reverse(int[] nums,int start,int end){
        int temp;
        while(start<end){
            temp=nums[start];
            nums[start]=nums[end];
            nums[end]=temp;
            start++;
            end--;
        }
    }
}
```
## Method3: 最初想到的方法 时间O(n) 空间O(1) 思路是对的 没有考虑完全 以至于没有把代码完善出来 教训是 找一个eg 一步一步把基本情况都罗列出来 得到一个完整的情况 
### 对于这道题 首先从起始位置开始 每次跳n 然后把他们放到下一个位置 回到起点的时候 把起点往前挪一个位置 开始下一个circle 外面用一个for循环只要操作N次就可以了
```python
class Solution(object):
    def rotate(self, nums, k):
        """
        :type nums: List[int]
        :type k: int
        :rtype: void Do not return anything, modify nums in-place instead.
        """
        n=len(nums)
        #special case
        if(k%n==0):
          return
        newIdx=0
        temp=nums[newIdx]
        circle=0
        for i in range(n):
          newIdx=(newIdx+k)%n
          temp,nums[newIdx]=nums[newIdx],temp
          if(circle==newIdx):
            newIdx+=1
            temp=nums[newIdx]
            
        

```

