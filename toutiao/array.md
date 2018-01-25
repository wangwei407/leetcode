```java

k sum问题 n to the power of k-1
//1.two sum
//167. Two Sum II - Input array is sorted
//15. 3Sum 返回的是没有重复
//18. 4Sum 3sum的迭代 注意几点 1.如何从开始避开重复 2.如何在找到答案挪动指针的时候避开重复
 public List<List<Integer>> fourSum(int[] nums, int target) {
        List<List<Integer>> ans=new ArrayList<>();
        Arrays.sort(nums);
        for(int i=0; i<nums.length-3;i++){
            if(i!=0 && nums[i]==nums[i-1]) continue;
            for(int j=i+1;j<nums.length-2;j++){
                if(j!=i+1 && nums[j]==nums[j-1]) continue;
                int t=j+1;
                int k=nums.length-1;
                while(t<k){
                    int result=nums[i]+nums[j]+nums[t]+nums[k];
                    if(target==result){
                        ans.add(new ArrayList(Arrays.asList(nums[i],nums[j],nums[t],nums[k])));
                        while(t<k && nums[t]==nums[t+1]) t++;
                        while(t<k && nums[k]==nums[k-1]) k--;
                        t++;
                        k--;
                    }else if(result > target){
                        k--;
                    }else{
                        t++;
                    }
                }
            }
        }
        return ans;
    }



//翻转问题
//189. Rotate Array
先找到新头部 然后开始rotate length-k%length
//151. Reverse Words in a String two pointers
//186. Reverse Words in a String II 和189一样 注意最后一段的处理
//61. Rotate List 旋转链表 先得找到长度 然后再判断k%len 是否为0 如果为0 不用旋转了
//153. Find Minimum in Rotated Sorted Array binary search
//154. Find Minimum in Rotated Sorted Array II 有重复的情况 有一种相等的情况
[3,3,1,3] 3=3 将最后边缩减一个位置
//33. Search in Rotated Sorted Array 先找到最小位置 然后再用binary search
不用关心其他问题 只要知道旋转了多少步 就可以把真实的mid位置找出来
public int search(int[] nums, int target) {
        int lo=0,hi=nums.length-1;
        while(lo<hi){
            int mid=lo+(hi-lo)/2;
            if(nums[mid]<nums[hi]) hi=mid;
            else {
                lo=mid+1;
            }
        }
        int minIdx=lo;
        int l=nums.length;
        if(target==nums[l-1]) return l-1;
        lo=(target<nums[l-1]) ? minIdx:0;
        hi=(target<nums[l-1]) ? l-1:minIdx-1;
        while(lo<=hi){
            int mid=lo+(hi-lo)/2;
            if(target==nums[mid]) return mid;
            else if(target<nums[mid]) hi=mid-1;
            else lo=mid+1;
        }
        return -1;
    }
    //81 Search in Rotated Sorted Array II 有重复元素
    三个注意点 
    lo<=hi 在指针移动的时候 防止少检查元素
    lo hi 移动的时候都要加1 防止指针不动
    如果中间元素和右边元素相等 记得要hi-- 因为不清楚是何种情况 可能是 3,3,3,3  也可以是3,1,3,3
    public boolean search(int[] nums, int target) {
        int lo=0,hi=nums.length-1;
        while(lo<=hi){
            int mid=lo+(hi-lo)/2;
            if(nums[mid]==target) return true;
            //right side sorted
            if(nums[mid]<nums[hi]){
                if(target>nums[mid] && target<=nums[hi]){
                    lo=mid+1;
                }else{
                    hi=mid-1;
                }
                //left side sorted
            }else if(nums[mid]>nums[hi]){
                if(target>=nums[lo] && target<nums[mid]){
                    hi=mid-1;
                }else{
                    lo=mid+1;
                }
            }else {
                hi--;
            }
            
        }
        return false;
    }

    //特殊形式的string  
    //isomorphic 同型问题 
    两个关键点 第一个是否和上次出现的对隐射一致 比如上次 a->c 这一次 a->b错误
    另一个点是 如果a->c 之前没有出现这个映射对 但是出现了c和其他的配对也是错误的
    //205. Isomorphic Strings
    //290. Word Pattern
    //291. Word Pattern II 待解决 backtrack


    //majority问题 1，2 用特殊算法来做 count为0 换元素 置为1
    method 1 sort return n/2


    //two pointer 移动问题
    //27. Remove Element
    //26. Remove Duplicates from Sorted Array 
    //283. Move Zeroes
    //80. Remove Duplicates from Sorted Array II


    //字符串转换成运算问题
    //66. Plus One
    //67. Add Binary 
    result=a^b^promote
    int val=a.charAt(i)-'0' 前面是int而不是char
    //2. Add Two Numbers 链表的
    //43. Multiply Strings 相乘问题
     int m=num1.length()-1,n=num2.length()-1;
        int pos[]=new int[m+n+2];
        for(int i=m;i>=0;i--){
            for(int j=n;j>=0;j--){
                int p1=i+j,p2=i+j+1;
                int ans=(num1.charAt(i)-'0')*(num2.charAt(j)-'0')+10*pos[p1]+pos[p2];
                pos[p1]=ans/10;
                pos[p2]=ans%10;
            }
        }
        StringBuilder result=new StringBuilder();
        for(int p:pos){
        	//result长度为0时 并且 pos里面也是0 不能往里加数字
            if(!(result.length()==0 && p==0)) result.append(p);
        }
        return result.length()==0? "0" : result.toString();
       //415. Add Strings
        //链表加一问题 369. Plus One Linked List
        ListNode ans=new ListNode(0),
        cur=head,
        lastNotNine=ans;
        ans.next=head;
        while(cur!=null){
            if(cur.val!=9){
            lastNotNine=cur;    
            }
            cur=cur.next;
        }
        lastNotNine.val+=1;
        cur=lastNotNine.next;
        
            while(cur!=null){
                  cur.val=0;
                cur=cur.next;
            }
            
   
        return ans.val==1? ans:ans.next;


        //contains duplicate 217 219 220
        if(nums.length<2 || k==0) return false;
        TreeSet<Long> set=new TreeSet<>();
        for(int i=0; i<nums.length; i++){
            if(i>k) set.remove((long) nums[i - k -1]);
            Long ceiling =set.ceiling((long)nums[i]);
            Long floor=set.floor((long)nums[i]);
            if((ceiling!=null && ceiling-nums[i]<=t) || (floor != null && nums[i]-floor<=t)) return true;
            set.add((long)nums[i]);
            
        }
        return false;
        //合并问题
 		//88. Merge Sorted Array 
 		//21. Merge Two Sorted Lists  
 		//23. Merge k Sorted 


 		//两个杨辉三角问题


 		//165. Compare Version Numbers


      //150. Evaluate Reverse Polish Notation 



        //k th element问题
        //4. Median of Two Sorted Arrays binary search 变相的找kth element
         public double findMedianSortedArrays(int[] n1, int[] n2) {
        int total=n1.length+n2.length;
        if(total%2==0) {
            return (getK(n1,n2,total/2,0,0)+getK(n1,n2,total/2+1,0,0))/2.0;
        }else{
            return getK(n1,n2,(total+1)/2,0,0);
        }
    }
    private int getK(int []n1,int[]n2, int k,int s1, int s2){
        if(s1>=n1.length){
            return  n2[s2+k-1];
        }
        if(s2>=n2.length){
            return n1[s1+k-1];
        }
        if(k==1){
            return Math.min(n1[s1],n2[s2]);
        }
        int m1=s1+k/2-1;
        int m2=s2+k/2-1;
        //idx
        //这里这样做 是抛弃了前K/2个元素 剩下的k也变小了 剩下的子问题还是在找k-k/2个元素 
        在k reach1之前 另一个超过元素的数组一定会被排除出去
        int mid1=m1<n1.length ? n1[m1] : Integer.MAX_VALUE;
        int mid2=m2<n2.length ? n2[m2] : Integer.MAX_VALUE;
        if(mid1<mid2){
            return getK(n1,n2,k-k/2,m1+1,s2);
        }else {
            return getK(n1,n2,k-k/2,s1,m2+1);
        }
        
    }

    //top k frequent 3种方法  一种比较好的方法 先放在map里 然后用一个桶 桶的索引是frquence
    public List<Integer> topKFrequent(int[] nums, int k) {
        List<Integer> ans=new ArrayList<>();
        Map<Integer,Integer> map=new HashMap<>();
        if(nums==null) return ans;
        
        for(int i=0; i<nums.length; i++){
            map.put(nums[i],map.getOrDefault(nums[i],0)+1);
        }
        List<Integer>[] hash=new List[nums.length+1];
        
        for(int num:map.keySet()){
            int freq=map.get(num);
            if(hash[freq]==null){
                hash[freq]=new LinkedList<Integer>();
            }
            hash[freq].add(num);
        }
        for(int i=hash.length-1; i>=0;i--){
            if(hash[i]!=null){
                for(int j=0;j<hash[i].size() && ans.size()<k;j++){
                    ans.add(hash[i].get(j));
                }
            }
        }
        return ans;
        
    }
    方法二
    public List<Integer> topKFrequent(int[] nums, int k) {
        Map<Integer, Integer> map = new HashMap<>();
        for(int n: nums){
            map.put(n, map.getOrDefault(n,0)+1);
        }
           
        PriorityQueue<Map.Entry<Integer, Integer>> maxHeap = 
                         new PriorityQueue<>((a,b)->(b.getValue()-a.getValue()));
        for(Map.Entry<Integer,Integer> entry: map.entrySet()){
            maxHeap.add(entry);
        }
        
        List<Integer> res = new ArrayList<>();
        while(res.size()<k){
            Map.Entry<Integer, Integer> entry = maxHeap.poll();
            res.add(entry.getKey());
        }
        return res;
    }

    方法三 treemap
     public List<Integer> topKFrequent(int[] nums, int k) {
        Map<Integer, Integer> map = new HashMap<>();
        for(int n: nums){
            map.put(n, map.getOrDefault(n,0)+1);
        }
        
        TreeMap<Integer, List<Integer>> freqMap = new TreeMap<>();
        for(int num : map.keySet()){
           int freq = map.get(num);
           if(!freqMap.containsKey(freq)){
               freqMap.put(freq, new LinkedList<>());
           }
           freqMap.get(freq).add(num);
        }
        
        List<Integer> res = new ArrayList<>();
        while(res.size()<k){
            Map.Entry<Integer, List<Integer>> entry = freqMap.pollLastEntry();
            res.addAll(entry.getValue());
        }
        return res;
    }



    //最大的kth 215. Kth Largest Element in an Array 
    第一种 直接排序 
    取nums[n-k]
    第二种 用一个优先队列 size为k 只要大于k  队列就往出排

    第三种 选择排序


    //最小的k th 在bst中 230. Kth Smallest Element in a BST

    中序遍历
    //top kth 






    //间隔问题
    //252. Meeting Rooms 看有没有overlap

    //253 Meeting rooms 3 看多少个能够把他们cover 
    先排序 然后用一个最小优先队列 往里放overlap的留在里面 overlap的自然放在了队伍的后面 然后不断的比较
    因为你start先进来 然后另一个进来的如果end比它早就放在前面了
    public int minMeetingRooms(Interval[] intervals) {
        if(intervals==null) return 0;
        if(intervals.length<2) return intervals.length;
       
        Arrays.sort(intervals, (a,b)->(a.start-b.start));
        
        PriorityQueue <Interval> q=new PriorityQueue<>(intervals.length,(a,b)->(a.end-b.end));
        
        int count=0;
        for(int i=0; i<intervals.length; i++){
            while(!q.isEmpty() && intervals[i].start>=q.peek().end)
                q.poll();
            q.offer(intervals[i]);
            count=Math.max(q.size(),count);
        }
        return count;
    }

    //56. Merge Intervals 把所有的overlap的都合并
    **关键是找到一个排序的方法

    public List<Interval> merge(List<Interval> is) {
         List<Interval> ans=new ArrayList<>();
         if(is==null || is.size()==0) return ans;
         
         Collections.sort(is,new Comparator<Interval>(){
             public int compare(Interval i1, Interval i2){
                 if(i1.start!=i2.start) return i1.start-i2.start;
                 else return i1.end-i2.end;
             }
         });
         Interval pre=is.get(0);
         for(int i=0; i<is.size();i++){
             Interval cur=is.get(i);
             if(pre.end<cur.start){
                 ans.add(pre);
                 pre=cur;
             }else{
                 pre=new Interval(pre.start,Math.max(cur.end,pre.end));
             }
         }
         ans.add(pre);
         return ans;
    }
    //57. Insert Interval
    三种情况 注意第二种是保持这个list有序
    public List<Interval> insert(List<Interval> intervals, Interval newi) {
         ArrayList<Interval> ans = new ArrayList<Interval>();
         for(Interval i: intervals){
             if(i.end < newi.start ){
                 ans.add(i);
             }else if(i.start>newi.end){
                 ans.add(newi);
                 newi=i;
             }else if(i.end>=newi.start || i.start<=newi.end){
                 newi=new Interval(Math.min(i.start,newi.start),Math.max(i.end,newi.end));
             }
         }
         ans.add(newi);
         return ans;
         
    }





        //字符串转数字

        //8. String to Integer (atoi)
        null or empty
        white space
        sign +/-
        calculate
        overflow

        括号问题 （）{}
        //20. Valid Parentheses
        最简单的问题 直接用栈来做
        //22. Generate Parentheses 给你括号的个数 让你创建所有的排列组合
        用backtrack来做
        //22. Generate Parentheses
        只要在当前右边的括号大于左边的话 这种情况是不对的 直接return
        public List<String> generateParenthesis(int n) {
        ArrayList<String> result = new ArrayList<String>();
        dfs(result, "", n, n);
        return result;
        }
        /*
        left and right represents the remaining number of ( and ) that need to be added. 
        When left > right, there are more ")" placed than "(". Such cases are wrong and the method stops. 
        */
        public void dfs(ArrayList<String> result, String s, int left, int right){
        if(left > right)
            return;

        if(left==0&&right==0){
            result.add(s);
            return;
        }

        if(left>0){
            dfs(result, s+"(", left-1, right);
        }

        if(right>0){
            dfs(result, s+")", left, right-1);
        }
        }

        //找出最长的一段valid 括号
        public int longestValidParentheses(String s) {
        int n = s.length(), longest = 0;
        Stack<Integer> st=new Stack<>();
        for (int i = 0; i < n; i++) {
            if (s.charAt(i) == '(') st.push(i);
            else {
                if (!st.empty()) {
                    if (s.charAt(st.peek()) == '(') st.pop();
                    else st.push(i);
                }
                else st.push(i);
            }
        }
        if (st.empty()) longest = n;
        else {
            int a = n, b = 0;
            while (!st.empty()) {
                b = st.peek(); st.pop();
                longest = Math.max(longest, a-b-1);
                a = b;
            }
            //corner case 
            longest = Math.max(longest, a);
        }
        return longest;
    }


    //最长问题
    //最长增长序列 经典问题
    //300. Longest Increasing Subsequence
    //5. Longest Palindromic Substring 找一个最长的回文子串
    dp[i][j]=s.charAt(i)==s.charAt(j) && (j-i<=2 || dp[i+1][j-1]) 问题是从哪里开始是理解的盲点
    dp[i][j]表示i到j是不是回文 
    i从高到低 因为需要用i+1推到i j从低到高因为需要从j+1推j
    public String longestPalindrome(String s) {
        int n=s.length();
        if(n==1) return s;
        boolean [][] dp=new boolean[n][n];
        String ans="";
        for(int i=n-1; i>=0;i--){
            for(int j=i;j<n;j++){
                dp[i][j]=s.charAt(i)==s.charAt(j) && (j-i<=2 || dp[i+1][j-1]);
                if(dp[i][j] && (j-i+1 > ans.length())) ans=s.substring(i,j+1);
            }
        }
        return ans;
    }

    //128. Longest Consecutive Sequence





    //排列问题按照字典顺序 字典序排序生成算法zig
    next permutation
    经典问题  
    分析这种过程，看后一个排列与前一个排列之间有什么关系？

    再如，设有排列(p)=2763541，按照字典式排序，它的下一个排列是什么？

    2763541 （找最后一个正序35）
    2763541 （找3后面比3大的最后一个数4）
    2764531 （交换3,4的位置）
    2764135 （把4后面的5,3,1反转）
    下面给出求 p[1…n] 的下一个排列的描述：

    求 i = max{j | p[j – 1] < p[j]} （找最后一个正序）
    求 j = max{k| p[i – 1] < p[k]} （找最后大于 p[i – 1] 的）
    交换 p[i – 1] 与 p[j]得到 p[1] … p[i-2] p[j] p[i] p[i+1] … p[j-1] p[i-1] p[j+1] … p[n]
    反转 p[j] 后面的数得到 p[1] … p[i-2] p[j] p[n] … p[j+1] p[i-1] p[j-1] … p[i]



    //sub问题 window问题 考察的是一定范围内的问题 (特点就是不间断 下面也有不间断的问题 就是相当于一个sub part)
    //209. Minimum Size Subarray Sum 维护一个window 不断的移动 求出所有的size 找出最小的
    两个pointer
    public int minSubArrayLen(int s, int[] nums) {
        int start=0,end=0,min=Integer.MAX_VALUE,l=nums.length,sum=0;
        while(end<l){
            sum+=nums[end];
            while(sum>=s){
                min=Math.min(min,l-i+1);
                sum-=nums[i--];
            }
            i--;
        }
    }

    //239. Sliding Window Maximum 
    解法一 window是个pq 空间复杂度O(k) 时间复杂度O(n*lgk) 如果k很大 GG
    public int[] maxSlidingWindow(int[] nums, int k) {
        if(k==0 || nums==null) return new int[0];
        int [] ans=new int[nums.length-k+1];
        PriorityQueue<Integer> pq=new PriorityQueue(k,new Comparator<Integer>(){
          public int compare(Integer a,Integer b){
              return b.compareTo(a);
          }  
        });
        for(int i=0;i<k;i++){
           pq.offer(nums[i]);
        }
        ans[0]=pq.peek();
        int i=0,j=k,idx=1;
        while(j<nums.length){
            pq.remove(nums[i++]);
            pq.offer(nums[j++]);
            ans[idx++]=pq.peek();
        }
        return ans;
    }
    解法二 线性时间复杂度  用一个deque 维持一个范围 [i-k+1,i]但是这个范围未必是deque里面有这么多元素
    放的只是候选的元素 如果a[i]>a[x] 那么我直接把她去了 因为他以后用不上 x从队尾开始往队头走
    比如 4 3 2 1 当3.5进来以后 3 2 1以后都不可能成为候选元素 直接删去
    public int[] maxSlidingWindow(int[] a, int k) {		
		if (a == null || k <= 0) {
			return new int[0];
		}
		int n = a.length;
		int[] r = new int[n-k+1];
		int ri = 0;
		// store index
		Deque<Integer> q = new ArrayDeque<>();
		for (int i = 0; i < a.length; i++) {
			// remove numbers out of range k
			while (!q.isEmpty() && q.peek() < i - k + 1) {
				q.poll();
			}
			// remove smaller numbers in k range as they are useless
			while (!q.isEmpty() && a[q.peekLast()] < a[i]) {
				q.pollLast();
			}
			// q contains index... r contains content
			q.offer(i);
			if (i >= k - 1) {
				r[ri++] = a[q.peek()];
			}
		}
		return r;
	}

    //76. Minimum Window Substring 一个意思 一个字典两个pointer解决
    public String minWindow(String s, String t) {
        if(s.length()<t.length()) return "";
        Map<Character,Integer> map=new HashMap<>();
        for(char c:s.toCharArray()){
             map.put(c,0);
        }
        for(char c:t.toCharArray()){
            if(!map.containsKey(c)) return "";
            map.put(c,map.get(c)+1);
        }
        
        int start=0,end=0,l=s.length(),counter=t.length(),min=Integer.MAX_VALUE,minStart=0;
        
        while(end<l){
            char c=s.charAt(end);
            
            if (map.get(c)>0){
                counter--;
            }
             map.put(c,map.get(c)-1);
            end++;
            while(counter==0){
                if(min>end-start){
                    min=end-start;
                    minStart=start;
                }
                char temp=s.charAt(start);
                map.put(temp,map.get(temp)+1);
                if(map.get(temp)>0) counter++;
                start++;
            }
        }
        return min==Integer.MAX_VALUE? "":s.substring(minStart,min+minStart);
    }
    //159. Longest Substring with At Most Two (k)Distinct Characters 同理 一个字典 两个
     public int lengthOfLongestSubstringTwoDistinct(String s) {
        int l=s.length();
        if(l==0) return 0;
        Map<Character,Integer> hash=new HashMap<Character, Integer>();
        int ans=0;
        for(int i=0,j=0; i<l; i++){
            char c=s.charAt(i);
            hash.put(c,hash.getOrDefault(c,0)+1);
            while(hash.size()>2){
                char left=s.charAt(j);
                hash.put(left,hash.get(left)-1);
                if(hash.get(left)==0) hash.remove(left);
                j++;
            }
            ans=Math.max(ans,i-j+1);
        }
        return ans;
        
    }
    //3. Longest Substring Without Repeating Characters
    public int lengthOfLongestSubstring(String s) {
        if (s.length()==0) return 0;
        HashMap<Character, Integer> map = new HashMap<Character, Integer>();
        int max=0;
        for(int i=0,j=0; i<s.length(); i++){
            char key=s.charAt(i);
            如果发现重复的
            if(map.containsKey(key)) {
                //如果重复的在j之前 说明不在当前window里 如果大于j说明在 需要把j挪到重复的字母前
                j=Math.max(j,map.get(key)+1);
            }
            map.put(key,i);
            max=Math.max(i-j+1,max);
        }
        return max;
       
    }
    未完待续
    //这个没法用two pointer 因为他不是一个定的window 用分治法 
    也就是找出频率小于k的 因为这些字母肯定不在答案上 
    395. Longest Substring with At Least K Repeating Characters
    {
    if(s==null || s.length()<k) return 0;
        if(k==1) return s.length();
        int [] map=new int[26];
        for(char c:s.toCharArray()){
            map[c-'a']++;
        }
        char bad=0;
        for(int i=0; i<26;i++){
            if(map[i]!=0 && map[i]<k){
                bad=(char)(i+'a');
                break;
            }
        }
        if(bad==0) return s.length();
        String[] group=s.split(bad+"");
        int res=0;
        for(String str:group){
            res=Math.max(longestSubstring(str,k),res);
        }
        return res;
    }
    30. Substring with Concatenation of All Words 未完待续

    346. Moving Average from Data Stream 
    MovingAverage m = new MovingAverage(3);
	m.next(1) = 1
	m.next(10) = (1 + 10) / 2
	m.next(3) = (1 + 10 + 3) / 3
	m.next(5) = (10 + 3 + 5) / 3

	用一个指针insert 超出数组长度就取余 当数组满了的时候 指向那个该删去的元素 用sum 来记录总和 然后减去指针指向的该删去的元素
	public double next(int val){
		if(n<window.length) n++;
		sum-=window[insert];
		sum+=val;
		window[insert]=val;
		insert=(insert+1)%window.length;
		return sum/n;
	}




    找出交集
    349. Intersection of Two Arrays
    350. Intersection of Two Arrays II
    160. Intersection of Two Linked Lists


    二分查找
    162. Find Peak Element
     public int findPeakElement(int[] nums) {
        return help(nums,0,nums.length-1);
    }
    public int help(int []nums,int start,int end){
        if(start==end) return end;
        else if(start+1==end) return nums[start]>nums[end] ? start:end;
        else{
            int mid=start+(end-start)/2;
            if(nums[mid]>nums[mid-1] && nums[mid]>nums[mid+1]) return mid;
            else if(nums[mid-1]<nums[mid] && nums[mid]<nums[mid+1]) return help(nums,mid+1,end);
            else  return help(nums,start,mid-1);
        }
    }

    127 word ladder 问题











    










```
