# LeetCode.724.寻找数组的中心索引

给定一个整数类型的数组 nums，请编写一个能够返回数组“中心索引”的方法。

我们是这样定义数组中心索引的：数组中心索引的左侧所有元素相加的和等于右侧所有元素相加的和。

如果数组不存在中心索引，那么我们应该返回 -1。如果数组有多个中心索引，那么我们应该返回最靠近左边的那一个。

##### 示例 1:

> 输入:
>
> nums = [1, 7, 3, 6, 5, 6]
>
> 输出: 3 
>
> 解释:
>
> 索引3 (nums[3] = 6) 的左侧数之和(1 + 7 + 3 = 11)，与右侧数之和(5 + 6 = 11)相等。
>
> 同时, 3 也是第一个符合要求的中心索引。

##### 示例 2:

> 输入:
>
> nums = [1, 2, 3]
>
> 输出: -1 
>
> 解释:
>
> 数组中不存在满足此条件的中心索引。

##### 说明:

nums 的长度范围为 [0, 10000]。

任何一个 nums[i] 将会是一个范围在 [-1000, 1000]的整数。

分析：

抓住问题核心，该元素左边总和等于该元素右边总和即为“中心索引”，如果每次遇到一个数把其左边全部加起来，再把右边全部加起来，时间复杂度为 O(n^2)，超时

考虑优化，既然左边右边数不变，可以开两个数组分别保存“当前元素左边元素总和”和“当前元素右边总和”，之后再遍历时，直接比较两数组当前值是否相等，依然超时

再考虑，既然左边的和都求出来了，右边的和不就是 总和 - 左边的元素总和 - 当前数组索引处的值，省去了计算“当前元素右边总和”。

时间复杂度为O(n)。

```java
class Solution {

    public int pivotIndex(int[] nums) {
        int sum = 0;
        for (int i = 0; i < nums.length; i++) {
            sum += nums[i];
        }
        int tmpSum = 0;
        for (int i = 0; i < nums.length; i++) {

            if (tmpSum == sum - tmpSum - nums[i]) {
                return i;
            }
            tmpSum += nums[i];
        }
        return -1;
    }
}
```