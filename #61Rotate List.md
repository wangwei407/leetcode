# Given a list, rotate the list to the right by k places, where k is non-negative.

For example:
Given 1->2->3->4->5->NULL and k = 2,
return 4->5->1->2->3->NULL.
## Method 最笨的办法 基本思想无非是找到新的头结点 把头结点的上一个结点的末尾变成null 然后把末尾结点连接点原来的头结点的前面
```python
class Solution(object):
    def rotateRight(self, head, k):
        """
        :type head: ListNode
        :type k: int
        :rtype: ListNode
        """
        #get the num of nodelist
        length=0
        tempH=head
        while tempH is not None:
            tempH=tempH.next
            length+=1
        if(length==0):
            return head
        if(k%length==0):
            return head
        tempH=head
        newStart=length-(k%length)+1
        start=1
        #get the privious newStart nodeList
        while  start<(newStart-1):
            tempH=tempH.next
            start+=1
        newHead=tempH.next
        #the last of listnode is null
        tempH.next=None
        #find the last node
        tempNew=newHead
        while(start<length-1):
            tempNew=tempNew.next
            start+=1
        tempNew.next=head    
        return newHead
```
### 链表的搜索总结
因为链表的next操作会使得当前结点改变 所以要求length 
```python
length=0
while Node is not None:
  Node=Node.next
  length+=1
```  
> 每次返回的是一个当前的结点next 长度算的是截止到当前结点的长度
查找链表的第n个元素 从第一个结点开始的话 每次会fetch到下一个结点 如果要查找第K个结点的话
```python
start=1
while 
  
