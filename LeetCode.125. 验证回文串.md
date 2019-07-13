# LeetCode.125. 验证回文串

**题目描述：**

给定一个字符串，验证它是否是回文串，只考虑字母和数字字符，可以忽略字母的大小写。

说明：本题中，我们将空字符串定义为有效的回文串。

示例 1:

```
输入: "A man, a plan, a canal: Panama"
输出: true
```


示例 2:

```
输入: "race a car"
输出: false
```

**解答：**

```java
// 时间复杂度：O(n)
// 空间复杂度：O(1)
class Solution {
    public boolean isPalindrome(String s) {
        
    if(s == null)
        return false;
    
    if(s.trim().length() == 0)
        return true;
    
    int left = 0;
    int right = s.length() - 1;
    s = s.toLowerCase();
    while(left <= right){
        if(s.charAt(left) == s.charAt(right)){
             left++;
             right--;
        } else if(s.charAt(left) < '0' || s.charAt(left) > 'z' || ('9' < s.charAt(left) && s.charAt(left)< 'a')) {
             left++;
        } else if(s.charAt(right) < '0' || s.charAt(right) > 'z' || ('9' < s.charAt(right) && s.charAt(right)< 'a')) {
             right--;
        } else {
             return false;
        }
    }
    return true;
  }
}
```

