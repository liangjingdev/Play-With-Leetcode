# Leetcode.49. 字母异位词分组

#### **方法一：排序数组分类**

**思路**

当且仅当它们的排序字符串相等时，两个字符串是字母异位词。 

**算法**

维护一个映射 ans : {String -> List}，其中每个键 K 是一个排序字符串，每个值是初始输入的字符串列表，排序后等于 K。 

在 Java 中，我们将键存储为字符串，例如，code。 在 Python 中，我们将键存储为散列化元组，例如，('c', 'o', 'd', 'e')。 

```java
代码 
class Solution { 

    public List<List<String>> groupAnagrams(String[] strs) { 

        if (strs.length == 0) return new ArrayList(); 

        Map<String, List> ans = new HashMap<String, List>(); 

        for (String s : strs) { 
            char[] ca = s.toCharArray(); 
            Arrays.sort(ca); 
            String key = String.valueOf(ca); 
            if (!ans.containsKey(key)) 
               ans.put(key, new ArrayList()); 
            ans.get(key).add(s); 
        } 
        return new ArrayList(ans.values()); 
    } 
} 
```

**复杂度分析**

时间复杂度：O(NKlogK)，其中 N 是 strs 的长度，而 K 是 strs 中字符串的最大长度。当我们遍历每个字符串时，外部循环具有的复杂度为 O(N)。然后，我们在 O(KlogK) 的时间内对每个字符串排序。 

空间复杂度：O(NK)，排序存储在 ans 中的全部信息内容。 



#### **方法二：按计数分类**

**思路**

当且仅当它们的字符计数（每个字符的出现次数）相同时，两个字符串是字母异位词。 

**算法**

我们可以将每个字符串 s 转换为字符数 count，由26个非负整数组成，表示 a，b，c 的数量等。我们使用这些计数作为哈希映射的基础。 

在 Java 中，我们的字符数 count 的散列化表示将是一个用 **＃** 字符分隔的字符串。 例如，abbccc 将表示为 ＃1＃2＃3＃0＃0＃0 ...＃0，其中总共有26个条目。  

在 python 中，表示将是一个计数的元组。 例如，abbccc 将表示为 (1,2,3,0,0，...，0)，其中总共有 26 个条目。 

```java
代码 

class Solution { 

    public List<List<String>> groupAnagrams(String[] strs) { 

        if (strs.length == 0) return new ArrayList(); 

        Map<String, List> ans = new HashMap<String, List>(); 
        int[] count = new int[26]; 

        for (String s : strs) { 
            Arrays.fill(count, 0); 
            for (char c : s.toCharArray()) 
               count[c - 'a']++; 

            StringBuilder sb = new StringBuilder(""); 

            for (int i = 0; i < 26; i++) { 
                sb.append('#'); 
                sb.append(count[i]); 
            } 

            String key = sb.toString(); 
            if (!ans.containsKey(key)) 
               ans.put(key, new ArrayList()); 

            ans.get(key).add(s); 
        } 
        return new ArrayList(ans.values()); 
    } 
} 
```

**复杂度分析**

时间复杂度：O(NK)，其中 N 是 strs 的长度，而 K 是 strs 中字符串的最大长度。计算每个字符串的字符串大小是线性的，我们统计每个字符串。 

空间复杂度：O(NK)，排序存储在 ans 中的全部信息内容。 



#### **方法三：算术基本定理**

**思路**

算术基本定理，又称为正整数的唯一分解定理，即：每个大于1的自然数，要么本身就是质数，要么可以写为2个以上的质数的积，而且这些质因子按大小排列之后，写法仅有一种方式。 

利用这个，我们把每个字符串都映射到一个正数上。 

**算法**

用一个数组存储质数 prime = {2, 3, 5, 7, 11, 13, 17, 19, 23, 29, 31, 41, 43, 47, 53, 59, 61, 67, 71, 73, 79, 83, 89, 97, 101, 103}。 

然后每个字符串的字符减去 ' a ' ，然后取到 prime 中对应的质数，把它们累乘。 

例如 abc ，就对应 'a' - 'a'， 'b' - 'a'， 'c' - 'a'，即 0, 1, 2，也就是对应素数 2 3 5，然后相乘 2 * 3 * 5 = 30，就把 "abc" 映射到了 30。 



```java
代码 

public List<List<String>> groupAnagrams(String[] strs) { 

    HashMap<Integer, List<String>> hash = new HashMap<>(); 

    //每个字母对应一个质数 

    int[] prime = { 2, 3, 5, 7, 11, 13, 17, 19, 23, 29, 31, 41, 43, 47, 53, 59, 61, 67, 71, 73, 79, 83, 89, 97, 101, 103 }; 

    for (int i = 0; i < strs.length; i++) { 
        int key = 1; 

        //累乘得到 key 
        for (int j = 0; j < strs[i].length(); j++) { 
            key *= prime[strs[i].charAt(j) - 'a']; 
        } 

        if (hash.containsKey(key)) { 
            hash.get(key).add(strs[i]); 
        } else { 
            List<String> temp = new ArrayList<String>(); 
            temp.add(strs[i]); 
            hash.put(key, temp); 
        } 
    } 

    return new ArrayList<List<String>>(hash.values()); 
} 
```

**复杂度分析**

时间复杂度：O（NK），K 是字符串的最长长度。 

空间复杂度：O（NK），用来存储结果。 

这个解法时间复杂度，较解法一有提升，但是有一定的局限性，因为求 key 的时候用的是累乘，可能会造成溢出，超出 int 所能表示的数字。 