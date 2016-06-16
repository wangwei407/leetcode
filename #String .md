#String
[345 Reverse Vowels of a String](#345)  
[151 Reverse Words in a String](#151)  
[205 Isomorphic Strings](#205)
#<a name="345">345 Reverse Vowels of a String</a>

## Write a function that takes a string as input and reverse only the vowels of a string.

Example 1:
Given s = "hello", return "holle".

Example 2:
Given s = "leetcode", return "leotcede"

### 思路：和单纯的reverse string思路一样 只不过这次的两个指针是在元音字母上移动
#### java solution
```java
public class Solution {
    public static String reverseString(String s){
	int l=s.length();
	if(l==0 || l==1 ) return s;
	String vowels="aeiouAEIOU";
	char[] ans=s.toCharArray();
	int start=0,end=l-1;
	while(start<end) {
	    while(start<end && !vowels.contains(ans[start]+"")){
		start++;    
	    }
	    while(start<end && !vowels.contains(ans[end]+"")){
		end--;
	    }
	    char temp=ans[start];
	    ans[start]=ans[end];
	    ans[end]=temp;
	    start++;
	    end--;
	}
	return ans.toString();
    }
}
```
#### python solution
```python
#345
class Solution(object):
    def reverseVowels(self, s):
        """
        :type s: str
        :rtype: str
        """
        vowels="aeiouAEIOU"
        ans=list(s)
        start,end=0,len(ans)-1
        while start<end:
            while start<end and ans[start] not in vowles:
                start+=1
            while start<end and ans[end] not in vowles:
                end-=1
            ans[start],ans[end]=ans[end],ans[start]
            start+=1
            end-=1
        return ''.join(ans)    
```   
# <a name="151">151. Reverse Words in a String</a>
## Given an input string, reverse the string word by word.

For example,
Given s = "the sky is blue",
return "blue is sky the".
### 思路 two pointer 一个pointer来遍历整个string 另一个pointer来标记每次的单词 添加到stringbuilder里

#### java solution
```java 
public class Solution {
    public String reverseWords(String s) {
        String str=s.trim();
        if (str.length()==0 || str.length()==1) return str;
        StringBuilder ans=new StringBuilder();
        int end=str.length()-1;
        int start=end;
        while(start>=0){
                while (start!=-1 && str.charAt(start)!= ' ') {
                    start--;
                }
            ans.append(str.substring(start+1,end+1)+" ");
            while( start!=-1 && str.charAt(start)==' '){
                start--;
            }
            end=start;
        }
        return ans.deleteCharAt(ans.length()-1).toString();
        
    }
}
```

#### python solution
```python
class Solution(object):
    def reverseWords(self, s):
    	return " ".join(s.split()[::-1])
```

# <a name="205">205. Isomorphic Strings</a>
## Given two strings s and t, determine if they are isomorphic.

Two strings are isomorphic if the characters in s can be replaced to get t.

All occurrences of a character must be replaced with another character while preserving the order of characters. No two characters may map to the same character but a character may map to itself.

For example,
Given "egg", "add", return true.

Given "foo", "bar", return false.

Given "paper", "title", return true.

Note:
You may assume both s and t have the same length.

### 思路：用hash来映射 有一个问题 如果单纯用单方向隐射 比如a->a 当第一个string出现b的时候 比如b->a 没法验证这种一一对应关系 解决这个问题的方法用一个hashmap 当遇见b的时候 判断一下现在hashmap里有没有a这个值 然后在建立b->a这个映射关系

### 还有一种思路：每次我们检查上一次看见的两个元素是不是和上一次是对应的 
#### java solution
```java
public boolean isIsomorphic(String s1, String s2) {
    Map<Character, Integer> m1=new HashMap<>();
    Map<Character, Integer> m2=new HashMap<>();
    for(Integer i=0; i<s1.length(); i++){
	if(m1.put(s1.charAt(i),i)!=m2.put(s2.charAt(i),i)){
	    return false;
	}
    }
    return true;
}
public boolean isIsomorphic(String s1,String s2){
    int[] map=new int[512];
    for(int i=0; i<s1.length(); i++){
	if(map[s1.charAt(i)]!=map[s2.charAt(i)+256]) return false;
	map[s1.charAt(i)]=map[s2.charAt(i)+256]=i+1;
    }
}
```
#### java solution
```python
def isIsomorphic1(self, s, t):
    d1, d2 = {}, {}
    for i, val in enumerate(s):
        d1[val] = d1.get(val, []) + [i]
    for i, val in enumerate(t):
        d2[val] = d2.get(val, []) + [i]
    return sorted(d1.values()) == sorted(d2.values())

def isIsomorphic2(self, s, t):
    d1, d2 = [[] for _ in xrange(256)], [[] for _ in xrange(256)]
    for i, val in enumerate(s):
        d1[ord(val)].append(i)
    for i, val in enumerate(t):
        d2[ord(val)].append(i)
    return sorted(d1) == sorted(d2)

def isIsomorphic3(self, s, t):
    return len(set(zip(s, t))) == len(set(s)) == len(set(t))

def isIsomorphic4(self, s, t): 
    return [s.find(i) for i in s] == [t.find(j) for j in t]

def isIsomorphic5(self, s, t):
    return map(s.find, s) == map(t.find, t)

def isIsomorphic(self, s, t):
    d1, d2 = [0 for _ in xrange(256)], [0 for _ in xrange(256)]
    for i in xrange(len(s)):
        if d1[ord(s[i])] != d2[ord(t[i])]:
            return False
        d1[ord(s[i])] = i+1
        d2[ord(t[i])] = i+1
    return True
```
