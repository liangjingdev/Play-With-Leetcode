# LeetCode.451. 根据字符出现频率排序

**题目描述：**

给定一个字符串，请将字符串里的字符按照出现的频率降序排列。

示例 1:

```
输入:
"tree"

输出:
"eert"

解释:
'e'出现两次，'r'和't'都只出现一次。
因此'e'必须出现在'r'和't'之前。此外，"eetr"也是一个有效的答案。
```

示例 2:

```
输入:
"cccaaa"

输出:
"cccaaa"

解释:
'c'和'a'都出现三次。此外，"aaaccc"也是有效的答案。
注意"cacaca"是不正确的，因为相同的字母必须放在一起。
```

示例 3:

```
输入:
"Aabb"

输出:
"bbAa"

解释:
此外，"bbaA"也是一个有效的答案，但"Aabb"是不正确的。
注意'A'和'a'被认为是两种不同的字符。
```

**题目解答：**

统计字符出现的频数可以使用辅助数组来做记录，这题中的关键是根据字符的出现频数来重新构建一个新的字符串，在于怎么选择map中的键值对（K-V）, 那么map的键可以用频数，则值就用字符的集合。

```java
// 假设字符串s的长度为n
// 时间复杂度：O(n)
// 空间复杂度：O(n)
class Solution {
    public String frequencySort(String s) {
        
    if(s == null || s.length() == 0)
        return s;
    
    int n = s.length();
    Map<Integer,List<Character>> map = new HashMap<>();
    int[] freq = new int[256];
    
    // 统计每个字符出现的频次
    for(char c : s.toCharArray())
        freq[c]++;
    
    for(int i = 0 ; i < 256 ; i++){
        if(freq[i] == 0)
            continue;
        if(!map.containsKey(freq[i]))
            map.put(freq[i],new ArrayList());
        map.get(freq[i]).add((char)i);
    }
    
    StringBuilder sb = new StringBuilder();
    for(int i = n ; i >= 1 ; i--){
        if(map.containsKey(i)){
            for(char c : map.get(i)){
                for(int j = 0 ; j < i ; j++)
                    sb.append(c);
            }
        }
    }
    return sb.toString();
  }
}
```