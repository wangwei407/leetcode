# leetcode
##Catogory: 
### 21. Merge Two Sorted Lists
#### Merge two sorted linked lists and return it as a new list. The new list should be made by splicing together the nodes of the first two lists.
##### 基本思想 1）使用merge的思想 2）如果有一个列表为空了 就把后面的列表续在后面 3）引用的注意 先找出头 把头保存起来 然后对temp做操作
e.g
```python
#先把head找到 保存起来 然后在对temp做操作 不会改变head的结构 但是head的next会随着temp的改变而改变
head=temp
temp=temp.next
```
#####递归求解
```python
def mergeTwoLists(self, l1, l2):
        """
        :type l1: ListNode
        :type l2: ListNode
        :rtype: ListNode
        """
        if not l1:
            return l2
        if not l2:
            return l1

        start = None    
        if l1.val < l2.val:
            start = l1;
            start.next = self.mergeTwoLists(l1.next, l2)
        else:
            start = l2;
            start.next = self.mergeTwoLists(l1, l2.next)

        return start
```    
##### java的简单求解
```java
public ListNode mergeTwoLists(ListNode l1, ListNode l2) {
    ListNode dummy = new ListNode(-1);
    ListNode cur = dummy;
    cur.next =  l1;
    while(l1 != null && l2 != null) {
        if(l1.val > l2.val) {
            cur.next = l2;
            l2 = l1;
        }
        cur = cur.next;
        l1 = cur.next;
    }
    if(l2 != null) cur.next = l2;
    return dummy.next;
}
```


