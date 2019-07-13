# LeetCode.344. 反转字符串

**题目描述：**

编写一个函数，以字符串作为输入，反转该字符串中的元音字母。

示例 1:

```
输入: "hello"
输出: "holle"
```


示例 2:

```
输入: "leetcode"
输出: "leotcede"
```

说明:
元音字母不包含字母"y"。

**解答：**

```java
// 时间复杂度：O(n)
// 空间复杂度：o(n)
class Solution {

public String reverseVowels(String s) {
    if(s.length() == 0 || s.length() == 1)
        return s;
    int left = 0;
    int right = s.length() - 1;
    char[] array = s.toCharArray();
    char temp = array[left];        
    while(left < right){
        if((array[left] != 'a' && array[left] != 'o' && array[left] != 'e' && array[left] != 'i' && array[left] != 'u'
          && array[left] != 'A' && array[left] != 'O' && array[left] != 'E' && array[left] != 'I' && array[left] != 'U'))
            left++;
        else if((array[right] != 'a' && array[right] != 'o' && array[right] != 'e' && array[right] != 'i' && array[right] != 'u'
               && array[right] != 'A' && array[right] != 'O' && array[right] != 'E' && array[right] != 'I' && array[right] != 'U'))
            right--;
        else {
            temp = array[left];
            array[left++] = array[right];
            array[right--] = temp;
         }
    }
    return s.valueOf(array);
  }

}
```