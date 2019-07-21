# LeetCode.205. 同构字符串

**题目描述：**

给定两个字符串 s 和 t，判断它们是否是同构的。

如果 s 中的字符可以被替换得到 t ，那么这两个字符串是同构的。

所有出现的字符都必须用另一个字符替换，同时保留字符的顺序。两个字符不能映射到同一个字符上，但字符可以映射自己本身。

示例 1:

```
输入: s = "egg", t = "add"
输出: true
```


示例 2:

```
输入: s = "foo", t = "bar"
输出: false
```


示例 3:

```
输入: s = "paper", t = "title"
输出: true
```


说明:
你可以假设 s 和 t 具有相同的长度。

**题目解答：**

```java
// 假设字符串t的长度为n
// 时间复杂度：O(n)
// 空间复杂度：O(n)
class Solution {
    public boolean isIsomorphic(String s, String t) {
        if(s == null && t == null)
            return true;
    
    Map<Character,Character> map = new HashMap<>();

    if(s.length() != t.length())
        return false;

    for(int i = 0 ; i < t.length() ; i++){
        char temp = s.charAt(i);
        char c = t.charAt(i);
        if(!map.containsKey(temp) && !map.containsValue(c)){                
            map.put(temp,c);            
        }else if(map.containsKey(temp) && map.get(temp).equals(c)){
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

