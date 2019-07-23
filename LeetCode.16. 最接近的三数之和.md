# LeetCode.16. 最接近的三数之和

**题目描述：**

给定一个包括 n 个整数的数组 nums 和 一个目标值 target。找出 nums 中的三个整数，使得它们的和与 target 最接近。返回这三个数的和。假定每组输入只存在唯一答案。

```
例如，给定数组 nums = [-1，2，1，-4], 和 target = 1.

与 target 最接近的三个数的和为 2. (-1 + 2 + 1 = 2).
```

**题目解答：**

```java
// 时间复杂度：O(n^2)
// 空间复杂度：O(1)
class Solution {
    public int threeSumClosest(int[] nums, int target) {
        if(nums == null || nums.length < 3)
            return 0;
        final int ARRAY_LOOP_INDEX_LIMIT = nums.length - 2;
        int result = 0;
        int dis = Integer.MAX_VALUE;
        Arrays.sort(nums);
        for(int i = 0 ; i < ARRAY_LOOP_INDEX_LIMIT ; i++){
            if(i > 0 && nums[i] == nums[i-1])
                continue;
            int l = i + 1;
            int r = nums.length - 1;
            while(l < r){
                int temp = (nums[i] + nums[l] + nums[r]);
                int k = Math.abs(target - temp);
                if(k <= dis){
                    dis = k;
                    result = temp;
                }
                if(temp >= target)
                    r--;
                else
                    l++;
            }
        }
        return result;
    }
}
```