```java

/**
交换排序 冒泡 快速
**/
//bubble sort (stable)
public void bubbleSort(int [] a){
		int length=a.length;
		for (int i=1; i<length ;i++ ) {
			for (int j=0; j<length-i ;j++ ) {
				if(a[j]>a[j+1]){
					int temp=a[j];
					a[j]=a[j+1];
					a[j+1]=temp;
				}
			}
		}
}

//改进 用了个flag
public void bubbleSort1(int [] a){
	int len=a.length;
	int temp=0;
	boolean flag=true;
	while(flag){
		flag=false;
		for (int i=0; i<length-1 ;i++ ) {
			if(a[j]>a[j-1]){
				falg=true;
			}
		}
	}
}
//快速排序 O(nlogn) O(n2) quick sort  unstable
public static void quickSort(int a[],low,high){
	if(low<high){
		int mid=help(a,low,high);
		quickSort(a,low,mid-1);
		quickSort(a,mid+1,high);
	}
}
private int help(int a[],int low,int high){
	int pivot=a[high];
	while(low<high){
		while(low<high && pivot<=a[high]) high--;
		a[low]=a[high];
		while(low<high && pivot>=a[low]) low--;
		a[high]=a[low];
	}
	a[low]=pivot;
	return high;
}
/**
插入排序 直接插入排序 希尔排序
**/
//希尔排序 不稳定
void ShellInsertSort(int a[], int n, int dk)  
{  
    for(int i= dk; i<n; ++i){  
        if(a[i] < a[i-dk]){          //若第i个元素大于i-1元素，直接插入。小于的话，移动有序表后插入  
            int j = i-dk;     
            int x = a[i];           //复制为哨兵，即存储待排序元素  
            a[i] = a[i-dk];         //首先后移一个元素  
            while(x < a[j]){     //查找在有序表的插入位置  
                a[j+dk] = a[j];  
                j -= dk;             //元素后移  
            }  
            a[j+dk] = x;            //插入到正确位置  
        }  
        print(a, n,i );  
    }  
      
}  
  
/** 
 * 先按增量d（n/2,n为要排序数的个数进行希尔排序 
 * 
 */  
void shellSort(int a[], int n){  
  
    int dk = n/2;  
    while( dk >= 1  ){  
        ShellInsertSort(a, n, dk);  
        dk = dk/2;  
    }  
}  
//插入排序 稳定
public static void insertSort(int a[],int n){
	//从1到n-1 这些元素都要往前插一下
	for(int i=1; i<n;i++){
		int j;
		for(j=i-1;j>=0;j--){
			if(a[j]<a[i]) break;
		}
		//find the position
		if(j!=i-1){
			int temp=a[i];
			//move element from index  i to j+2
			for(int k=i;k>j+1;j--){
				a[k]=a[k-1];
			}
			a[j+1]=temp;
		}
		}
	}
}
//优化算法
public static void insertSort(int a[],int n){
	int j;
	for(int i=1;i<n;i++){
		//need move
		if(a[i]<a[i-1]){
			int tmp=a[i];
			for(j=i-1;j>=0 && a[j]>tmp;j++){
				a[j+1]=a[j];
			}
			//j现在的位置是排好序的位置 所以要j+1
			a[j+1]=temp;
		}
	}
}


/**
选择排序  简单选择排序 堆排序

**/

//选择排序
public static void findMin(int a[],int n,int i){
	int k=i;
	for(int j=i+1;j<n;j++){
		if(a[k]>a[j]) k=j;
	}
	return k;
}
public static void selectSort(int a[],int n){
	int key,tmp;
	for(int i=0;i<n;i++){
		key=findMin(a,n,i);
		//find min which is not in the index i,do swap
		if(key!=i){
			tmp=a[i];
			a[i]=a[key];
			a[key]=tmp;

		}
	}
}
//改进选择排序
void SelectSort(int r[],int n) {  
    int i ,j , min ,max, tmp;  
    for (i=1 ;i <= n/2;i++) {    
        // 做不超过n/2趟选择排序   
        min = i; max = i ; //分别记录最大和最小关键字记录位置  
        for (j= i+1; j<= n-i; j++) {  
            if (r[j] > r[max]) {   
                max = j ; continue ;   
            }    
            if (r[j]< r[min]) {   
                min = j ;   
            }     
      }    
      //该交换操作还可分情况讨论以提高效率  
      tmp = r[i-1]; r[i-1] = r[min]; r[min] = tmp;  
      tmp = r[n-i]; r[n-i] = r[max]; r[max] = tmp;   
  
    }   
}  



/**
归并排序
**/
public void merge()

//链表的排序
//148. Sort List (merge sort)
 public ListNode sortList(ListNode head) {
        if(head==null || head.next==null) return head;
        ListNode pre=head,slow=head,fast=head;
        while(fast!=null && fast.next!=null){
            pre=slow;
            slow=slow.next;
            fast=fast.next.next;
        }
        pre.next=null;
        ListNode l1=sortList(head);
        ListNode l2=sortList(slow);
        return merge(l1,l2);
    }
//147. Insertion Sort List(insert sort)
     public ListNode insertionSortList(ListNode head) {
        if(head==null || head.next==null) return head;
        ListNode ans=new ListNode(0),pre=ans,cur=head,next=null;
        while(cur!=null){
            //stroe
            next=cur.next;
            //find the position
            while(pre.next!=null && pre.next.val<cur.val){
                pre=pre.next;
            }
            //insert
            cur.next=pre.next;
            pre.next=cur;
            pre=ans;
            cur=next;
        }
        return ans.next;
    }

 //75. Sort Colors  数组内有3种元素 按照从小到大顺序排列 1.counter 2.two pointers
     public void sortColors(int[] nums) {
        int n=nums.length;
        int p0=-1,p1=-1,p2=-1;
        for(int i=0;i<n;i++){
            if(nums[i]==0){
                nums[++p2]=2;
                nums[++p1]=1;
                nums[++p0]=0;
            }else if(nums[i]==1){
                nums[++p2]=2;
                nums[++p1]=1;
            }else {
                nums[++p2]=2;
            }
        }
    }
//179. Largest Number 用string组数字
    public String largestNumber(int[] nums) {
 		if(nums.length==0 || nums==null) return "";
        String[] store=new String[nums.length];
        for(int i=0; i<nums.length;i++){
            store[i]=String.valueOf(nums[i]);
        }
        //compator的写法
	   Comparator<String> comp=new Comparator<String>(){
	       public int compare(String str1,String str2){
	           String s1=str1+str2;
	           String s2=str2+str1;
	           return s2.compareTo(s1);
	       }
	   };
	   Arrays.sort(store,comp);
	     if(store[0].charAt(0) == '0')
                    return "0";
	   StringBuilder sb=new StringBuilder();
	   for(String str:store){
	       sb.append(str);
	   }
	   return sb.toString();
}


//大小替换
```
