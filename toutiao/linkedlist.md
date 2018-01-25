```java
// 求单链表中结点的个数  
    // 注意检查链表是否为空。时间复杂度为O（n）  
    public static int getListLength(Node head) {  
    	if(head == null) return 0;
    	int len=0;
    	Node cur=head;
    	while(cur != null){
    		len++;
    		cur=cur.next;
    	}
    	return len;
    }
 // 翻转链表（遍历）  
    // 从头到尾遍历原链表，每遍历一个结点，  
    // 将其摘下放在新链表的最前端。  
    // 注意链表为空和只有一个结点的情况。时间复杂度为O（n）  
    public static Node reverseList(Node head) {  
    	if(head == null || head.next == null ) return head;
    	Node reHead=null,cur=head;

    	while(cur!=null){
    		Node pre=cur;
    		cur=cur.next;
    		pre.next=reHead;
    		reHead=pre;
    	}
    	return reHead;
    }
    //recursive method
      public static Node reverseListRec(Node head){  
      	if(head == null || head.next == null) return head;
      	 /* 
         head 
            1 -> 2 -> 3 -> 4 
         
          head 
            1-------------- 
                                | 
                   4 -> 3 -> 2                            // Node reHead = reverseListRec(head.next); 
               reHead      head.next 
             
                   4 -> 3 -> 2 -> 1                    // head.next.next = head; 
               reHead 
                
                    4 -> 3 -> 2 -> 1 -> null            // head.next = null; 
               reHead 
     */  
      	Node reHead=reverseListRec(head.next);
      	head.next.next=head;
      	head.next=null;
      	return reHead;
      }

//查找单链表中的倒数第K个结点（k > 0） 
  public static Node reGetKthNode(Node head, int k) {  
  	if(head==0 || k==0) return head;
  	Node p=head,q=head;
  	while(k>1 && q!=null){
  		q=q.next;
  		k--;
  	}
  	if(k>1 || q==null){
  		return null;
  	}
  	while(q.next!=null){
  		p=p.next;
  		q=q.next;
  	}
  	return p;
  }
  // recursive method
  static int level=0;
   public static void reGetKthNodeRec(Node head, int k) { 
   } 

  // 查找单链表的中间结点  
    public static Node getMiddleNode(Node head) { 
    	if (head == null || head.next == null) {  
            return head;  
        }  
        Node runner=head,walker=head;
        while(runner.next != null && runner.next.next!=null){
        	runner=runner.next.next;
        	walker=walker.next;
        }
        return walker;
     } 
 //从尾到头打印单链表 
  public static void reversePrintListStack(Node head) { 
  	Stack<Node> s=new Stack();
  	Node cur=haed;
  	whle(cur!=null){
  		s.push(cur);
  		cur=cur.next;
  	}
  	while(!s.empty()){
  		cur=s.pop();
  		print(cur.val);
  	}
   } 
// recursive method
public static void reversePrintListRec(Node head) { 
	if(head==null) return ;
	else{
		reversePrintListRec(head.next);
		print(head.val);
	}
}      

//合并两个有序的单链表
public static Node mergeSortedList(Node head1, Node head2){
	 // 其中一个链表为空的情况，直接返回另一个链表头，O(1)  
        if (head1 == null) {  
            return head2;  
        }  
        if (head2 == null) {  
            return head1;  
        }  
        Node ans=null;
        //find head of ans
        if(head1.val < head2.val){
        	ans=head1;
        	head1=head1.next;
        	ans.next=null;
        } else{
        	ans=head2;
        	head2=head2.next;
        	ans.next=null;
        }
        Node cur=ans;
        //merge
        while(head1 != null && head2 != null){
        	if(head1.val<head2.val){
        		cur.next=head1;
        		head1=head1.next;
        		cur=cur.next;
        		cur.next=null;
        	}else{
        		cur.next=head2;
        		head2=head2.next;
        		cur=cur.next;
        		cur.next=null;
        	}
        }
        if(head1!=null){
        	cur.next=head1;
        }else if (head2!=null) {
        	cur.next=head2;
        }
        return ans;

}
//recursive method
 public static Node mergeSortedListRec(Node head1, Node head2) {  
        if (head1 == null) {  
            return head2;  
        }  
        if (head2 == null) {  
            return head1;  
        }  
        Node ans=null;
        if(head1.val > head2.val){
        	ans=head1;
        	ans.next=mergeSortedListRec(head1.next,head2);
        }else{
        	ans=head2;
        	ans.next=mergeSortedListRec(head1,head2.next);
        }
        return ans;
    }
// 判断一个单链表中是否有环 
     public static boolean hasCycle(Node head) { 
     	Node runnner=head,walker=head;
     	while(runnner != null && runnner.next!=null){
     		runnner=runnner.next.next;
     		walker=walker.next;
     		if(walker==runnner) return true;
     	}
     	return false;
      }

//判断是否相交 找出最后一个节点是否相同
public static boolean isIntersect(Node head1, Node head2) {
	 if (head1 == null || head2 == null) {  
            return false;  
        }  
  
        Node tail1 = head1;  
        // 找到链表1的最后一个节点  
        while (tail1.next != null) {  
            tail1 = tail1.next;  
        }  
  
        Node tail2 = head2;  
        // 找到链表2的最后一个节点  
        while (tail2.next != null) {  
            tail2 = tail2.next;  
        }  
  
        return tail1 == tail2;  
 }

   /** 
     * 求两个单链表相交的第一个节点 对第一个链表遍历，计算长度len1，同时保存最后一个节点的地址。 
     * 对第二个链表遍历，计算长度len2，同时检查最后一个节点是否和第一个链表的最后一个节点相同，若不相同，不相交，结束。 
     * 两个链表均从头节点开始，假设len1大于len2 
     * ，那么将第一个链表先遍历len1-len2个节点，此时两个链表当前节点到第一个相交节点的距离就相等了，然后一起向后遍历，直到两个节点的地址相同。 
     * 时间复杂度，O(len1+len2) 
     *  
     *              ----    len2 
     *                   |__________ 
     *                   | 
     *       ---------   len1 
     *       |---|<- len1-len2 
     */  
    public static Node getFirstCommonNode(Node head1, Node head2) { 
    	  if (head1 == null || head2 == null) {  
            return null;  
        }  
        	int len=1;
        	Node tail1=head1;
        	while(tail1.next!=null){
        		tail1=tail1.next;
        		len1++;
        	}
        	int len2 = 1;  
        Node tail2 = head2;  
        while (tail2.next != null) {  
            tail2 = tail2.next;  
            len2++;  
        }  
  
        // 不相交直接返回NULL  
        if (tail1 != tail2) {  
            return null;  
        }  
        Node n1=head1;
        Node n2=head2;
        if(len1>len2){
        	int k=len1-len2;
        	while(k!=0){
        		n1=n1.next;
        		k--;
        	}	
        } else {  
            int k = len2 - len1;  
            while (k != 0) {  
                n2 = n2.next;  
                k--;  
            }  
        }  
         while (n1 != n2) {  
            n1 = n1.next;  
            n2 = n2.next;  
        }  
        return n1;

     }
   /** 
     * 求进入环中的第一个节点 用快慢指针做（本题用了Crack the Coding Interview的解法，因为更简洁易懂！） 
     */  
    public static Node getFirstNodeInCycle(Node head) {  
        Node slow = head;  
        Node fast = head;  
  
        // 1） 找到快慢指针相遇点  
        while (fast != null && fast.next != null) {  
            slow = slow.next;  
            fast = fast.next.next;  
            if (slow == fast) { // Collision  
                break;  
            }  
        }  
  
        // 错误检查，这是没有环的情况  
        if (fast == null || fast.next == null) {  
            return null;  
        }
         slow = head;  
        while (slow != fast) {  
            slow = slow.next;  
            fast = fast.next;  
        }  
  
        // 再次相遇点就是环的开始处  
        return fast;    
    }
    ** 
     * 求进入环中的第一个节点 用HashMap做 一个无环的链表，它每个结点的地址都是不一样的。 
     * 但如果有环，指针沿着链表移动，那这个指针最终会指向一个已经出现过的地址 以地址为哈希表的键值，每出现一个地址，就将该键值对应的实值置为true。 
     * 那么当某个键值对应的实值已经为true时，说明这个地址之前已经出现过了， 直接返回它就OK了 
     */  
    public static Node getFirstNodeInCycleHashMap(Node head) {  
        HashMap<Node, Boolean> map = new HashMap<Node, Boolean>();  
        while (head != null) {  
            if (map.get(head) == true) {  
                return head; // 这个地址之前已经出现过了，就是环的开始处  
            } else {  
                map.put(head, true);  
                head = head.next;  
            }  
        }  
        return head;  
    }  

//reverse 问题
 // 206. Reverse Linked List  234. Palindrome Linked List
    //234的代码 注意其中reverse的代码 容易搞错
   public class Solution {
    public boolean isPalindrome(ListNode head) {
        if(head==null || head.next ==null) return true;
       ListNode wk=head,run=head,mid=head.next,pre=wk;
       while(run.next!=null && run.next.next!=null){
           run=run.next.next;
           pre=wk;
           wk=mid;
           mid=mid.next;
           wk.next=pre;
       }
       if(run.next==null){
           wk=wk.next;
       }
       while(mid!=null){
           if(wk.val!= mid.val) return false;
           wk=wk.next;
           mid=mid.next;
       }
       return true;
    }
}

//删除节点问题 可以把后面的节点的值放在当前节点 然后删除后面的节点
//237. Delete Node in a Linked List 
//203. Remove Linked List Elements
//83. Remove Duplicates from Sorted List 如果和下一个相同 删下一个 指针不移动 反则移动一下指针
//82. Remove Duplicates from Sorted List II 这个问题是把所有相同的删去(two pointers)
//86. Partition List 将小于x的元素放在前面 （two pointers）
public class Solution { //82
    public ListNode deleteDuplicates(ListNode head) {
        if(head==null || head.next==null) return head;
        ListNode nHead=new ListNode(0);
        nHead.next=head;
        ListNode pre=nHead,cur=head;
        while(cur!=null){
            while(cur.next!=null && cur.val==cur.next.val){
                cur=cur.next;
            }
            if(pre.next==cur){
                pre=pre.next;
            }else{
                pre.next=cur.next;
            }
            cur=cur.next;
        }
        return nHead.next;
        
    }
}

public ListNode partition(ListNode head, int x) {、、86
        if(head==null) return head;
        ListNode d1=new ListNode(0),d2=new ListNode(0),t1=d1,t2=d2;
        while(head!=null){
            if(head.val<x){
                t1.next=head;
                t1=head;
            }else{
                t2.next=head;
                t2=head;
            }
            head=head.next;
        }
        t2.next=null;
        t1.next=d2.next;
        return d1.next;
    }


//环的问题
//141. Linked List Cycle
//142. Linked List Cycle II 找焦点

//list相交问题
public class Solution {
    public ListNode getIntersectionNode(ListNode headA, ListNode headB) {
        if(headA==null || headB==null) return null;
        ListNode p=headA,q=headB;
        while (p!=q) {
            p= p == null? headB : p.next;
            q= q == null? headA : q.next;
        }
        return p;
    }
}


//倒数问题 19. Remove Nth Node From End of List
//92. Reverse Linked List II 给出m到n 分割开来
//https://discuss.leetcode.com/topic/8976/simple-java-solution-with-clear-explanation
//61. Rotate List 1.找出length 2.找出新开头（新开头前一位的.next 置为0） 3.遍历到后面接上head 
//143 reorder  L0→Ln→L1→Ln-1→L2→Ln-2→… 1.找中间 2.颠倒后面 3.插进来

//颠倒pair问题 定义一个新头
public class Solution {
    public ListNode swapPairs(ListNode head) {
        if(head == null || head.next==null) return head;
        ListNode h=new ListNode(0);
        h.next=head;
        ListNode p=h;
        while (p.next != null && p.next.next != null) {
            ListNode tmp=p;
             p=p.next;
              tmp.next=p.next;
              p.next=p.next.next;
              tmp.next.next=p;
        }
        return h.next;
        
    }
}


//bst 转化问题 
//108. Convert Sorted Array to Binary Search Tree
//109. Convert Sorted List to Binary Search Tree
public TreeNode sortedListToBST(ListNode head) {//109
        if(head==null) return null;
        return help(head,null);
    }
    public TreeNode help(ListNode low,ListNode high){
        if(low==high) return null;
        ListNode slow=low,fast=low;
        while(fast.next!=high && fast.next.next!=high){
            slow=slow.next;
            fast=fast.next.next;
        }
        TreeNode node=new TreeNode(slow.val);
        node.left=help(low,slow);
        node.right=help(slow.next,high);
        return node;
    }
    public TreeNode sortedArrayToBST(int[] nums) {//109
        return help(nums,0,nums.length-1);
    }
    public TreeNode help(int []nums,int low,int high){
       if (low>high) return null;
       int mid=low+(high-low)/2;
       TreeNode node=new TreeNode(nums[mid]);
       node.left=help(nums,low,mid-1);
       node.right=help(nums,mid+1,high);
       return node;
    }

```
