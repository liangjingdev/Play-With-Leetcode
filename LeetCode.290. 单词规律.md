# LeetCode.290. 单词规律

**题目描述：**

给定一种规律 pattern 和一个字符串 str ，判断 str 是否遵循相同的规律。

这里的 遵循 指完全匹配，例如， pattern 里的每个字母和字符串 str 中的每个非空单词之间存在着双向连接的对应规律。

示例1:

```
输入: pattern = "abba", str = "dog cat cat dog"
输出: true
```


示例 2:

```
输入:pattern = "abba", str = "dog cat cat fish"
输出: false
```


示例 3:

```
输入: pattern = "aaaa", str = "dog cat cat dog"
输出: false
```


示例 4:

```
输入: pattern = "abba", str = "dog dog dog dog"
输出: false
```


说明:
你可以假设 pattern 只包含小写字母， str 包含了由单个空格分隔的小写字母。    

**题目解答：**

```java
// 假设字符串pattern的长度为n
// 时间复杂度：O(n)
// 空间复杂度：O(n)
class Solution {
    public boolean wordPattern(String pattern, String str) {
        
    if(pattern == null && str == null)
        return true;
    
    Map<Character,String> map = new HashMap<>();
    // 对字符串str按照空白符进行分割
    String[] s = str.split("\\s+");
    
    if(pattern.length() != s.length)
        return false;
    
    for(int i = 0 ; i < pattern.length() ; i++){
        char temp = pattern.charAt(i);
        if(!map.containsKey(temp) && !map.containsValue(s[i])){                
            map.put(temp,s[i]);            
        }else if(map.containsKey(temp) && map.get(temp).equals(s[i])){
            // 注意这里要使用equals方法来进行判断，equals方法比较的是字符串的内容是否相同
            // '=='有时候会由于a和b指向两个不同的对象而返回false(a和b的内容相同)
            continue;
        }else
            return false;
    }
    return true;
  }
}
```