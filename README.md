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


