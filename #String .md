#String
[345 Reverse Vowels of a String](#345)  
[151 Reverse Words in a String](#151)
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
