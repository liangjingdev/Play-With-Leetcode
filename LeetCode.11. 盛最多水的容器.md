# LeetCode.11. 盛最多水的容器

**题目描述：**

给定 n 个非负整数 a1，a2，...，an，每个数代表坐标中的一个点 (i, ai) 。在坐标内画 n 条垂直线，垂直线 i 的两个端点分别为 (i, ai) 和 (i, 0)。找出其中的两条线，使得它们与 x 轴共同构成的容器可以容纳最多的水。

说明：你不能倾斜容器，且 n 的值至少为 2。

![image-20190714095738412](http://ww3.sinaimg.cn/large/006tNc79ly1g4z4vuwb28j30o80c6t92.jpg)

图中垂直线代表输入数组 [1,8,6,2,5,4,8,3,7]。在此情况下，容器能够容纳水（表示为蓝色部分）的最大值为 49。

示例:

```
输入: [1,8,6,2,5,4,8,3,7]
输出: 49
```

**解答：**

```java
// 时间复杂度：O(n)
// 空间复杂度：O(1)
// 双索引技术
class Solution {
    public int maxArea(int[] height) {
        if(height.length <= 1)
            return 0;
        int left = 0;
        int right = height.length - 1;
        int maxVolume = 0;
        while(left < right){
            if(height[left] <= height[right]){
                maxVolume = (right-left)*height[left] > maxVolume ? (right-left)*height[left] : maxVolume;
                left++;
            }else if(height[left] > height[right]){
                maxVolume = (right-left)*height[right] > maxVolume ? (right-left)*height[right] : maxVolume;
                right--;
            }
         }
        return maxVolume;
    }
}
```