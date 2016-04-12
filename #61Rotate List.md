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
从链表的第N个 查找第k个结点（k>=n）
因为从起始结点第一次next就返回的是下一个结点 所以我们只要做K-N次就可以完成操作 因为range函数range(n,k)返回的就是n,n+1,...k-1 也就是k-n次

```python
for index in range(N,k)
    Node=Node.next
```
### 修改过程 后来发现在计算长度的时候 可以把查找末尾结点和它合并起来
```python
length=1
while Node.next is not None:
    Node=Node.next
    length+=1
此时Node是末尾结点
```
## 不用计算length的方法
感觉有点麻烦 先放一下
### Java solution
```java
public class Solution {
    public ListNode rotateRight(ListNode head, int k) {
        //special case
        if(head==null || head.next==null || k==0)
            return head;
        //calculate the length of list and find the last node
        int length=1;
        ListNode tempH=head;
        while(tempH.next!=null){
            tempH=tempH.next;
            length++;
        }
        if(k%length==0){
            return head;
        }
        ListNode tempLast=tempH;
        //connect head and tail
        tempLast.next=head;
        int newStartIdx=length-(k%length)+1;
        //find the former node of the new start node
        tempH=head;
        for (int index=1; index<newStartIdx-1;index++){
            tempH=tempH.next;
        }
        ListNode newHead=tempH.next;
        tempH.next=null;
        return newHead;
        
    }
}
```

