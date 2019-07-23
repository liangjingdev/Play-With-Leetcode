# LeetCode.18. 四数之和

**题目描述：**

给定一个包含 n 个整数的数组 nums 和一个目标值 target，判断 nums 中是否存在四个元素 a，b，c 和 d ，使得 a + b + c + d 的值与 target 相等？找出所有满足条件且不重复的四元组。

注意：

答案中不可以包含重复的四元组。

示例：

```
给定数组 nums = [1, 0, -1, 0, -2, 2]，和 target = 0。

满足要求的四元组集合为：
[
  [-1,  0, 0, 1],
  [-2, -1, 1, 2],
  [-2,  0, 0, 2]
]
```

**题目解答：**

```java
// 时间复杂度：O(n^2)
// 空间复杂度：O(n)
class Solution {
    public List<List<Integer>> fourSum(int[] nums, int target) {
        List<List<Integer>> result = new ArrayList<>();
        final int ARRAY_LENGTH_LOW_LIMIT = 4;
        final int OUTER_LOOP_INDEX_LIMIT = nums.length - 3;
        final int INNER_LOOP_INDEX_LIMIT = nums.length -2;       
        if(nums == null || nums.length < ARRAY_LENGTH_LOW_LIMIT)
            return result;
        // 对数组进行升序排序
        Arrays.sort(nums);
        for(int i = 0 ; i < OUTER_LOOP_INDEX_LIMIT ; i++){
            // 去重
            if(i > 0 && nums[i] == nums[i-1])
                continue;
            for(int j = i + 1 ; j < INNER_LOOP_INDEX_LIMIT ; j++){
                // 去重
                if(j > i+1 && nums[j] == nums[j-1])
                    continue;
                int l = j + 1;
                int r = nums.length - 1;
                int temp = target - nums[i] - nums[j];
                while(l < r){
                    if(nums[l]+nums[r] == temp){
                        result.add(Arrays.asList(nums[i],nums[j],nums[l],nums[r]));
                        while(l < r && nums[l] == nums[l+1])
                            l++;
                        while(l < r && nums[r] == nums[r-1])
                            r--;
                        l++;
                        r--;
                    }else if(nums[l]+nums[r] < temp){
                        l++;
                    }else{
                        r--;
                    }
                }
            }
        }
        return result;
    }
}
```