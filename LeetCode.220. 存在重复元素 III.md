# LeetCode.220. 存在重复元素 III

给定一个整数数组，判断数组中是否有两个不同的索引 i 和 j，使得 nums [i] 和 nums [j] 的差的绝对值最大为 t，并且 i 和 j 之间的差的绝对值最大为 ķ。

示例 1:

输入: [1,2,3,1], k = 4, t = 0

输出: true 

示例 2:

输入: [1,0,1,1], k = 1, t = 0

输出: true 

示例 3:

输入: [4,2], k = 2, t = 1

输出: false 

### 解题思路：

给定一个整数数组，判断其中是否存在两个不同的下标i和j，满足：| nums[i] - nums[j] | <= t 且下标：| i - j | <= k。

可以想到，维护一个大小为k的二叉搜索树BST，遍历数组中的元素，在BST上搜索有没有符合条件的数对，若存在则直接返回true，否则将当前元素数对插入BST，并更新这个BST（若此时BST的大小已为k，需要删掉一个值）。保证BST的大小小于或等于为k，是为了保证里面的数下标差值一定符合条件：| i - j | <= k。

------

这道题一眼看上去就知道要对一个滑动窗口为k的数组进行搜索，然后寻找与当前元素相差<t的元素。如果使用暴力搜索的话，时间复杂度为O(Nk)（大家可以算下）这个在k特别大的时候会TLE，所以必须对滑动窗口进行处理，理想情况下是组织成一棵树，而且最好是一个平衡二叉树。这样对元素的查找、删除和添加都是LOG(K)时间。如果用C实现，比较麻烦，所幸java中有treeset这个类，可以生成一个平衡二叉树而无需考虑实现细节。

代码如下，这里面注意：在nums[i]+t时可能发生溢出，需要将其强制转换为long类型。

```java
// 算法时间复杂度：O(nlogn)
// 空间复杂度：O(k)
class Solution {
    public boolean containsNearbyAlmostDuplicate(int[] nums, int k, int t) {
        TreeSet<Long> treeSet = new TreeSet<>();
        for(int i=0;i<nums.length;i++){
            if (treeSet.ceiling((long) nums[i] - (long) t) != null && (treeSet.ceiling((long) nums[i] - (long) t) <= ((long) nums[i] + (long) t)))
                return true;
            treeSet.add((long)nums[i]);
            if(treeSet.size() == (k+1))
                treeSet.remove((long)nums[i-k]);    
        }
        return false;
    }
}
```