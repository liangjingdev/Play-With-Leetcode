# LeetCode.202.快乐数

**题目描述：**

编写一个算法来判断一个数是不是“快乐数”。

一个“快乐数”定义为：对于一个正整数，每一次将该数替换为它每个位置上的数字的平方和，然后重复这个过程直到这个数变为 1，也可能是无限循环但始终变不到 1。如果可以变为 1，那么这个数就是快乐数。

示例: 

```
输入: 19
输出: true
解释: 
12 + 92 = 82
82 + 22 = 68
62 + 82 = 100
12 + 02 + 02 = 1
```

**题目解答：**

首先定义一个Set集合，用来存放计算后的平方和m，如果m在Set中已存在，即表示进入了死循环，则退出； 如果m不存在Set，则将m放入Set； 直至找到平方和为1或者进入死循环就退出。

```java
class Solution {
    public boolean isHappy(int n) {
        if(n == 0)
            return false;
        if(n == 1)
            return true;
        Set<Integer> set = new HashSet<>();
        int m = 0;
        while(true){
            while(n != 0){
                m += Math.pow(n%10,2);
                n /= 10;
            }
            if(m == 1)
                return true;
            if(set.contains(m))
                return false;
            set.add(m);
            n = m;
            m = 0;
        }
    }
}
```