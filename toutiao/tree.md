```java
/** 
 * http://blog.csdn.net/luckyxiaoqiang/article/details/7518888  轻松搞定面试中的二叉树题目 
 * http://www.cnblogs.com/Jax/archive/2009/12/28/1633691.html  算法大全（3） 二叉树 
 *  
 * TODO: 一定要能熟练地写出所有问题的递归和非递归做法！ 
 * 
 * 1. 求二叉树中的节点个数: getNodeNumRec（递归），getNodeNum（迭代） 
 * 2. 求二叉树的深度: getDepthRec（递归），getDepth  
 * 3. 前序遍历，中序遍历，后序遍历: preorderTraversalRec, preorderTraversal, inorderTraversalRec, postorderTraversalRec 
 * (https://en.wikipedia.org/wiki/Tree_traversal#Pre-order_2) 
 * 4.分层遍历二叉树（按层次从上往下，从左往右）: levelTraversal, levelTraversalRec（递归解法！） 
 * 5. 将二叉查找树变为有序的双向链表: convertBST2DLLRec, convertBST2DLL 
 * 6. 求二叉树第K层的节点个数：getNodeNumKthLevelRec, getNodeNumKthLevel 
 * 7. 求二叉树中叶子节点的个数：getNodeNumLeafRec, getNodeNumLeaf 
 * 8. 判断两棵二叉树是否相同的树：isSameRec, isSame 
 * 9. 判断二叉树是不是平衡二叉树：isAVLRec 
 * 10. 求二叉树的镜像（破坏和不破坏原来的树两种情况）：mirrorRec, mirrorCopyRec 
 * 10.1 判断两个树是否互相镜像：isMirrorRec 
 * 11. 求二叉树中两个节点的最低公共祖先节点：getLastCommonParent, getLastCommonParentRec, getLastCommonParentRec2 
 * 12. 求二叉树中节点的最大距离：getMaxDistanceRec 
 * 13. 由前序遍历序列和中序遍历序列重建二叉树：rebuildBinaryTreeRec 
 * 14.判断二叉树是不是完全二叉树：isCompleteBinaryTree, isCompleteBinaryTreeRec 
 *  
 */  


    /** 
     * 求二叉树中的节点个数递归解法： O(n) 
     * （1）如果二叉树为空，节点个数为0  
     * （2）如果二叉树不为空，二叉树节点个数 = 左子树节点个数 + 
     *            右子树节点个数 + 1 
     */  
    public void getNodeNumReC(TreeNode root){
    	if(head==null) return 0;
    	else {
    		return getNodeNumReC(root.left)+getNodeNumReC(root.right)+1;
    	}
    }

    //迭代算法
    public void getNodeNum(TreeNode root){
    	if (head==null) {
    		return 0;
    	}
    	int count=1;
    	Queue<TreeNode> q=new LinkedList<>();
    	q.add(root);

    	while(!q.isEmpty()){
    		TreeNode cur=q.poll();
    		if(cur.left!=null){
    			q.add(cur.left);
    			count++;
    		}if(cur.right!=null){
    			q.add(cur.right);
    			count++;
    		}
    	}
    	return count;
    }
 	/** 
     * 求二叉树的深度（高度） 递归解法： O(n) 
     * （1）如果二叉树为空，二叉树的深度为0  
     * （2）如果二叉树不为空，二叉树的深度 = max(左子树深度， 右子树深度) + 1 
     */  

 	public void getDepthRec(TreeNode root){
 		if(root==null) return 0;
 		return Math.max(getDepthRec(root.left),getDepthRec(root.right))+1;
 	}
 	//迭代方法
 	public void getDepth(TreeNode root){
 		if(root==null) return 0;
 		int currentLevel=1;
 		int nextLevel=0;
 		int depth=0;
 		Queue <TreeNode> q=new Queue<>();
 		q.add(root);
 		while(!q.isEmpty()){
 			TreeNode cur=q.poll();
 			currentLevel--;
 			if(cur.left!=null){
 				q.add(cur.left);
 				nextLevel++;
 			}if(cur.right!=null){
 				q.add(cur.right);
 				nextLevel++;
 			}if(currentLevel==0){
 				depth++;
 				currentLevel=nextLevel;
 				nextLevel=0;
 			}
 		}
 	}

    /** 
     * 前序遍历，中序遍历，后序遍历 前序遍历递归解法：  
     * （1）如果二叉树为空，空操作  
     * （2）如果二叉树不为空，访问根节点，前序遍历左子树，前序遍历右子树 
     */  
      public static void preorderTraversalRec(TreeNode root) {  
        if (root == null) {  
            return;  
        }  
        System.out.print(root.val + " ");  
        preorderTraversalRec(root.left);  
        preorderTraversalRec(root.right);  
    }  

    //
     public static void preorderTraversal(TreeNode root) { 
     	if(root==null) return ;
     	Stack<TreeNode> stack=new Stack<>();
     	stack.push(root);

     	while(!stack.isEmpty()){
     		TreeNode cur=stack.pop();
     		review(cur);
     		if(cur.right != null){
     			stack.push(right);
     		}if(cur.left!=null){
     			stack.push(left);
     		}
     	}
      }
     /** 
     * 中序遍历递归解法  
     * （1）如果二叉树为空，空操作。  
     * （2）如果二叉树不为空，中序遍历左子树，访问根节点，中序遍历右子树 
     */  
      public static void inorderTraversal(TreeNode root){ 
      	if(root == null) return ;
      	Stack<TreeNode> st=new Stack();
      	TreeNode cur=root;
      	while(true){
      		while(cur!=null){
      			st.push(cur);
      			cur=cur.left;
      		}
      		//没有左孩子
      		cur=st.pop();
      		review(cur);
      		cur=cur.right;
      	}
       }
       /** 
     * 后序遍历递归解法  
     * （1）如果二叉树为空，空操作  
     * （2）如果二叉树不为空，后序遍历左子树，后序遍历右子树，访问根节点 
     */  
    public static void postorderTraversalRec(TreeNode root) {  
        if (root == null) {  
            return;  
        }  
        postorderTraversalRec(root.left);  
        postorderTraversalRec(root.right);  
        System.out.print(root.val + " ");  
    }  
     public static void postorderTraversal(TreeNode root) {  
        if (root == null) {  
            return;  
        }  
          
        Stack<TreeNode> s = new Stack<TreeNode>();      // 第一个stack用于添加node和它的左右孩子  
        Stack<TreeNode> output = new Stack<TreeNode>();// 第二个stack用于翻转第一个stack输出  
          
        s.push(root);  
        while( !s.isEmpty() ){      // 确保所有元素都被翻转转移到第二个stack  
            TreeNode cur = s.pop(); // 把栈顶元素添加到第二个stack  
            output.push(cur);         
              
            if(cur.left != null){       // 把栈顶元素的左孩子和右孩子分别添加入第一个stack  
                s.push(cur.left);  
            }  
            if(cur.right != null){  
                s.push(cur.right);  
            }  
        }  
          
        while( !output.isEmpty() ){ // 遍历输出第二个stack，即为后序遍历  
            System.out.print(output.pop().val + " ");  
        }  
    }  



    //bfs 递归算法

    public static void levelTraversalRec(TreeNode root) {  
        ArrayList<ArrayList<Integer>> ret = new ArrayList<ArrayList<Integer>>();  
        dfs(root, 0, ret);  
        System.out.println(ret);  
    }  
    public void dfs(TreeNode root,int level,ArrayList<ArrayList<Integer>> ret){
    	if(root==null) return ;
    	if(level >= ret.size()){
    		ret.add(new ArrayList<Integer>());
    	}
    	ret.get(level).add(root.val);
    	dfs(root.left,level+1,ret);
    	dfs(root.right,level+1,ret);
    }
  /**
  
  */



//树的深度问题 bfs


//114. Flatten Binary Tree to Linked List
//199. Binary Tree Right Side View
//104. Maximum Depth of Binary Tree 
//111. Minimum Depth of Binary Tree bfs 如果某一个节点是根节点 直接ruturn
//102. Binary Tree Level Order Traversal bfs
//107. Binary Tree Level Order Traversal II 反序列  add(0,sub)
//110. Balanced Binary Tree 考察树是不是balance
//314. Binary Tree Vertical Order Traversal bfs 两个queue 一个node 一个col +一个map来根据col保存list
//103. Binary Tree Zigzag Level Order Traversal 每一层遍历的顺序不一样 定义一个forward变量
//226. Invert Binary Tree 交换树 迭代 递归
//100. Same Tree 递归 p.val==q.val && isSame(p.left,q.left) && isSame(p.right,q.right);
    //inorder stack 推进最左端点 然后判断栈空 然后pop端点 遍历pop端点的右子树
//98. Validate Binary Search Tree (inorder travels)
//94. Binary Tree Inorder Traversal
//285. Inorder Successor in BST 二叉树中比该结点大的最小节点
//173. Binary Search Tree Iterator 
//230. Kth Smallest Element in a BST
//114. Flatten Binary Tree to Linked List

    //preorder
//144. Binary Tree Preorder Traversal 用栈 先推右边 再推左边
//255. Verify Preorder Sequence in Binary Search Tree (stack)
    //postorder 两个stack 一个stack正常push 按照 根左右 再将其pop的结点push进另一个stack 
//145. Binary Tree Postorder Traversal

//已知两个遍历顺序构建原树问题(待完成)
/**
















**/

//255
public int kthSmallest(TreeNode root, int k) {//230
        Stack <TreeNode> s=new Stack<>();
        TreeNode p=root;
        while(p!=null){
            s.push(p);
            p=p.left;
        }
        while(k!=0){
            TreeNode pop=s.pop();
            k--;
            if(k==0) return pop.val;
            TreeNode right=pop.right;
            while(right!=null){
                s.push(right);
                right=right.left;
            }
        }
       return -1;
    }
 public List<List<Integer>> levelOrder(TreeNode root) {//102
        List<List<Integer>> ans=new ArrayList<>();
        if (root == null) return ans;
        Queue<TreeNode> q=new LinkedList<>();
        q.add(root);
        while (!q.isEmpty()){
            int size=q.size();
            List<Integer> sub=new LinkedList<>();
            for(int i=0;i<size;i++){
                if(q.peek().left!=null) q.add(q.peek.left);
                if(q.peek().right!=null) q.add(q.peek().right);
                sub.add(q.poll().val);
            }
            ans.add(sub);
        }
        return ans;       
    }
private int height(TreeNode root){//110
    if(root==null) return 0;
    int left=height(root.left);
    if(left==-1) return -1;
    int right=height(root.right);
    if(right==-1) return -1;
    if(Math.abs(left-right)>1) return -1;
    return Math.max(left,right)+1;
} 
public List<List<Integer>> verticalOrder(TreeNode root) {//314
        List<List<Integer>> ans=new ArrayList<>();
        if(root==null) return ans;
        Queue<TreeNode> q=new LinkedList<>();
        Queue<Integer> cols=new LinkedList<>();
        Map<Integer,List<Integer>> map=new HashMap<>();
        
        int max=0,min=0;
        q.add(root);
        cols.add(0);
        while(!q.isEmpty()){
            TreeNode cur=q.poll();
            int col=cols.poll();
            if(!map.containsKey(col)) map.put(col,new ArrayList<Integer>());
            map.get(col).add(cur.val);
            if(cur.left!=null){
                q.add(cur.left);
                cols.add(col-1);
                if(min>=col) min=col-1;
            }if(cur.right!=null){
                q.add(cur.right);
                cols.add(col+1);
                if(max<=col) max=col+1;
            }
        }
        for(int i=min;i<=max;i++){
            ans.add(map.get(i));
        }
        return ans;
    }
       public TreeNode invertTree(TreeNode root) {//226
        if (root == null) return root;
        TreeNode left=invertTree(root.left);
        TreeNode right=invertTree(root.right);
        root.left=right;
        root.right=left;
        return root;
    }

 //公共祖先问题 
 //235. Lowest Common Ancestor of a Binary Search Tree 根据这个搜索二叉树特性 左边小 右边大
 // 236. Lowest Common Ancestor of a Binary Tree 用一个map来定义父子关系 然后再用一个set来判断
     public TreeNode lowestCommonAncestor(TreeNode root, TreeNode p, TreeNode qq) {
        /**
        if (root == null || root == p || root == q) return root;
        TreeNode left=lowestCommonAncestor(root.left,p,q);
        TreeNode right=lowestCommonAncestor(root.right,p,q);
        if (left != null && right != null) return root;
        return left == null ? right:left;
        **/
        Map<TreeNode, TreeNode> parent=new HashMap<>();
        parent.put(root,null);
        Queue<TreeNode> q=new LinkedList<>();
        q.add(root);
        while(!parent.containsKey(p) || !parent.containsKey(qq)){
            TreeNode cur=q.poll();
            if(cur.left!=null){
                q.add(cur.left);
                parent.put(cur.left,cur);
            }if(cur.right!=null){
                q.add(cur.right);
                parent.put(cur.right,cur);
            }
        }
        Set<TreeNode> path=new HashSet<>();
        while(p!=null){
            path.add(p);
            p=parent.get(p);
        }
        while(!path.contains(qq)){
            qq=parent.get(qq);
        }
        return qq;
        
    }


//对称问题 
//101. Symmetric Tree    
    public boolean isSymmetric(TreeNode root) {//
        /**
        if (root == null) return true;
        return help(root.left,root.right);
        **/
        if(root==null) return true;
        Queue <TreeNode> q=new LinkedList<>();
        q.add(root.left);
        q.add(root.right);
        while (!q.isEmpty()) {
            TreeNode left=q.poll(),right=q.poll();
            if (left == null && right==null) continue;
            if(left == null ^ right == null) return false;
            if(left.val != right.val) return false;
            q.add(left.left);
            q.add(right.right);
            q.add(left.right);
            q.add(right.left);
        }
        return true;
        
    }
    private boolean help(TreeNode left,TreeNode right){
        if (left==null || right==null) return left == right;
        if (left.val != right.val) return false;
        return help(left.left,right.right) && help(left.right,right.left);
        
    }

//dfs问题
//250. Count Univalue Subtrees
//112. Path Sum 
//113. Path Sum II 找出所有的情况 backtrack
//404. Sum of Left Leaves 求左边的叶子节点的sum 判断左孩子是不是叶子 如果是 + left.val    
//257. Binary Tree Paths 
//129. Sum Root to Leaf Numbers 和257差不多 也可以用pre order 然后一边走 一边改左右孩子的value
//270. Closest Binary Search Tree Value 二叉树特性 
//222. Count Complete Tree Nodes
    public int countUnivalSubtrees(TreeNode root) {//250
        int [] count=new int[1];
        count[0]=0;
        help(root,count);
        return count[0];
    }
    public boolean help(TreeNode root,int [] count){
        if(root==null) return true;
        boolean left=help(root.left,count);
        boolean right=help(root.right,count);
        if(left && right){
            if(root.left!=null && root.val!=root.left.val) return false;
            if(root.right!=null && root.val!=root.right.val) return false;
            count[0]++;
            return true;
        }
        return false;
    }
    public int countNodes(TreeNode root) {//220
        int h=height(root);
        return h==-1 ? 0 : height(root.right) == h-1 ? (1<<h) + countNodes(root.right) : (1<<h-1) + countNodes(root.left);
    }
    public int height(TreeNode root){
        if (root == null) return -1;
        return 1+height(root.left);
    }    
    public List<List<Integer>> pathSum(TreeNode root, int sum) {//113
        List<List<Integer>> ans=new LinkedList<>();
        if(root==null) return ans;
        Stack<Integer> tmp =new Stack<>();
        help(ans,tmp,sum,root);
        return ans;
    }
    private void help(List<List<Integer>> ans,Stack<Integer> tmp,int sum,TreeNode root)
    {
        if(root==null) return;
        tmp.push(root.val);
        if(root.left==null && root.right==null) 
            if(root.val==sum) ans.add(new LinkedList<>(tmp));
            else {
                tmp.pop();
                return;
            }
        help(ans,tmp,sum-root.val,root.left);
        help(ans,tmp,sum-root.val,root.right);
        tmp.pop();
    }

    public int sumNumbers(TreeNode root) {//129
       
        return help(root,0);
    }
    public int help(TreeNode root,int sum){
       if (root == null) return 0;
       if (root.left == null && root.right == null) return sum*10+root.val;
       return help(root.left,sum*10+root.val)+help(root.right,sum*10+root.val);
    }

    public int closestValue(TreeNode root, double target) {//270
       int a=root.val;
       TreeNode kid=root.val>target ?  root.left:root.right;
       if(kid==null) return a;
       int b=closestValue(kid,target);
       return Math.abs(a-target)<Math.abs(b-target)? a:b;
       
    }


    //tree dp问题
    //96. Unique Binary Search Trees
    //95. Unique Binary Search Trees II
    for(int i=2;i<=n;i++){//96
            for(int j=1;j<=i;j++){
                dp[i]+=dp[j-1]*dp[i-j];
            }
        }

         public List<TreeNode> generateTrees(int n) {
        if(n==0) return new ArrayList<TreeNode>();
        return help(1,n);
    }
    private List<TreeNode> help(int start,int end){//95
        List<TreeNode> ans=new LinkedList<>();
        if(start>end){
            ans.add(null);
            return ans;
        }if(start==end){
            ans.add(new TreeNode(start));
            return ans;
        }
        for(int i=start;i<=end;i++){
            List<TreeNode> l=help(start,i-1);
            List<TreeNode> r=help(i+1,end);
            for(TreeNode lnode:l){
                for(TreeNode rnode:r){
                    TreeNode root=new TreeNode(i);
                    root.left=lnode;
                    root.right=rnode;
                    ans.add(root);
                }
            }
        }
        return ans;
    }



    //前缀树 211. Add and Search Word - Data structure design 
    //208. Implement Trie (Prefix Tree)
    public class WordDictionary {
    public class Trie{
        public Trie[] children=new Trie[26];
        String item="";
    }
    public Trie root=new Trie();
    // Adds a word into the data structure.
    public void addWord(String word) {
        Trie node=root;
        for(char c:word.toCharArray()){
            if(node.children[c-'a']==null){
                node.children[c-'a']=new Trie();
            }
            node=node.children[c-'a'];
        }
        node.item=word;
    }

    // Returns if the word is in the data structure. A word could
    // contain the dot character '.' to represent any one letter.
    public boolean search(String word) {
        return match(word.toCharArray(),0,root);
    }
    private boolean match(char[] cs, int offset,Trie node){
        if(offset==cs.length){
            return !node.item.equals("");
        }
        if(cs[offset]!='.'){
            return node.children[cs[offset]-'a']!=null && match(cs,offset+1,node.children[cs[offset]-'a']);
        }else{
            for(int i=0;i<node.children.length;i++){
                if(node.children[i]!=null && match(cs,offset+1,node.children[i])) return true;
            }
        }
        return false;
    }
}

```
