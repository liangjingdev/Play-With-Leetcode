# LeetCode.76. 最小覆盖子串

题目描述：

给你一个字符串 S、一个字符串 T，请在字符串 S 里面找出：包含 T 所有字母的最小子串。

示例：

```
输入: S = "ADOBECODEBANC", T = "ABC"
输出: "BANC"
```


说明：

如果 S 中不存这样的子串，则返回空字符串 ""。
如果 S 中存在这样的子串，我们保证它是唯一的答案。

**解答：**

```java
// 时间复杂度：O(m+n) m:s.length() n:t.length()
// 空间复杂度：O(n)
// 双索引技术+滑动窗口
class Solution {
    public String minWindow(String s, String t) {
        
    if (s.length() == 0 || t.length() == 0) {
		   return "";
	  }
    
    // 记录最小子串的开始位置，以及长度
    int start = -1;
    int minLen = s.length();
    int left = 0,right = 0;
    int match = 0;
    Map<Character,Integer> tMap = new HashMap<>();
    Map<Character,Integer> window = new HashMap<>();
    
    for(char c : t.toCharArray()){
        if(tMap.containsKey(c))
            tMap.put(c,tMap.get(c) + 1);
        else
            tMap.put(c,1);
    }
    
    while(right < s.length()){
        char c1 = s.charAt(right);
        if(tMap.containsKey(c1)){
            if(window.containsKey(c1))
                window.put(c1,window.get(c1) + 1);
            else 
                window.put(c1,1);
            if(tMap.get(c1) == window.get(c1))
                match++;
        }
        right++;
        
        while(match == tMap.size()){              
            if((right - left) <= minLen){
                minLen = right - left;
                start = left;
            }
            char c2 = s.charAt(left);
            if(tMap.containsKey(c2)){
                window.put(c2,window.get(c2) - 1);
                if(window.get(c2) < tMap.get(c2))
                    match--;
            }
            left++;
        }
    }
    return start == -1 ? "" : s.substring(start,start+minLen);
  }
}
```