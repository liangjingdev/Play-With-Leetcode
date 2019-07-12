# LeetCode.88. 合并两个有序数组

**题目描述：**

给定两个有序整数数组 nums1 和 nums2，将 nums2 合并到 nums1 中，使得 num1 成为一个有序数组。

说明:

初始化 nums1 和 nums2 的元素数量分别为 m 和 n。
你可以假设 nums1 有足够的空间（空间大小大于或等于 m + n）来保存 nums2 中的元素。
示例:

```
输入:
nums1 = [1,2,3,0,0,0], m = 3
nums2 = [2,5,6],       n = 3

输出: [1,2,2,3,5,6]
```

**解答：**    

```java
// 时间复杂度：O(m+n)
// 空间复杂度：O(m+n) 优化方法：双指针 / 从后往前 
// 从结尾处开始改写 nums1 的值又会如何呢？(从尾部开始遍历nums1数组)这里没有信息，因此不需要额外空间。O(1)
class Solution {
    public void merge(int[] nums1, int m, int[] nums2, int n) {
    // nums1数组的索引指针
    int p1 = 0;
    // nums2数组的索引指针
    int p2 = 0;
    // 辅助数组
    int[] nums = new int[m+n];
    // 辅助变量
    int i = 0;
    while(p1 < m || p2 < n){
        if(p1 == m && p2 < n)
            nums[i++] = nums2[p2++]; 
        else if(p1 < m && p2 == n)
            nums[i++] = nums1[p1++];
        else if(nums1[p1] <= nums2[p2])
            nums[i++] = nums1[p1++];
        else if(nums2[p2] < nums1[p1])
            nums[i++] = nums2[p2++];
    }
    for(i = 0 ; i < m+n ; i++)
        nums1[i] = nums[i];
   }
}
```
