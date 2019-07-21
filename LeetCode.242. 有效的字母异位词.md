# LeetCode.242. 有效的字母异位词

**题目描述：**

给定两个字符串 s 和 t ，编写一个函数来判断 t 是否是 s 的字母异位词。

示例 1:

```
输入: s = "anagram", t = "nagaram"
输出: true
```


示例 2:

```
输入: s = "rat", t = "car"
输出: false
```

说明:
你可以假设字符串只包含小写字母。

进阶:
如果输入字符串包含 unicode 字符怎么办？你能否调整你的解法来应对这种情况？

**解答：**

```java
// 时间复杂度：O(n)
// 空间复杂度：O(n)
class Solution {
    public boolean isAnagram(String s, String t) {
        
    Map<Character,Integer> sMap = new HashMap<>();
    
    if(s == null && t == null)
        return false;
    
    if(s.length() != t.length())
        return false;
    
    for(int i = 0 ; i < s.length() ; i++){
        char temp = s.charAt(i);
        if(!sMap.containsKey(temp))
            sMap.put(temp,1);
        else
            sMap.put(temp,sMap.get(temp) + 1);
    }
    
    for(int i = 0 ; i < t.length() ; i++){
        char temp = t.charAt(i);
        if(sMap.containsKey(temp) && sMap.get(temp) > 0)
            sMap.put(temp,sMap.get(temp) - 1);
        else
            return false;
    }
    return true;
  }
}
```

**方法一：排序**
算法： 通过将 s 的字母重新排列成 t 来生成变位词。因此，如果 T 是 S 的变位词，对两个字符串进行排序将产生两个相同的字符串。此外，如果 s 和 t 的长度不同，t 不能是 s 的变位词，我们可以提前返回。

```java
public boolean isAnagram(String s, String t) {
    if (s.length() != t.length()) {
        return false;
    }
    char[] str1 = s.toCharArray();
    char[] str2 = t.toCharArray();
    Arrays.sort(str1);
    Arrays.sort(str2);
    return Arrays.equals(str1, str2);
}
```

复杂度分析

时间复杂度：O(nlogn)，假设 n 是 s 的长度，排序成本 O(nlogn) 和比较两个字符串的成本 O(n)。排序时间占主导地位，总体时间复杂度为 O(nlogn)。

空间复杂度：O(1)，空间取决于排序实现，如果使用 heapsort，通常需要 O(1) 辅助空间。

注意，在 Java 中，toCharArray() 制作了一个字符串的拷贝，所以它花费 O(n) 额外的空间，但是我们忽略了这一复杂性分析，因为：

- 这依赖于语言的细节。

- 这取决于函数的设计方式。例如，可以将函数参数类型更改为 char[]。

**方法二：哈希表**

算法：

1、为了检查 t 是否是 s 的重新排列，我们可以计算两个字符串中每个字母的出现次数并进行比较。因为 S 和 T 都只包含 A-Z 的字母，所以一个简单的 26 位计数器表就足够了。
2、我们需要两个计数器数表进行比较吗？实际上不是，因为我们可以用一个计数器表计算 s 字母的频率，用 t 减少计数器表中的每个字母的计数器，然后检查计数器是否回到零。

```java
public boolean isAnagram(String s, String t) {
    if (s.length() != t.length()) {
        return false;
    }
    int[] counter = new int[26];
    for (int i = 0; i < s.length(); i++) {
        counter[s.charAt(i) - 'a']++;
        counter[t.charAt(i) - 'a']--;
    }
    for (int count : counter) {
        if (count != 0) {
            return false;
        }
    }
    return true;
}
```

3、或者我们可以先用计数器表计算 s，然后用 t 减少计数器表中的每个字母的计数器。如果在任何时候计数器低于零，我们知道 t 包含一个不在 s 中的额外字母，并立即返回 FALSE。