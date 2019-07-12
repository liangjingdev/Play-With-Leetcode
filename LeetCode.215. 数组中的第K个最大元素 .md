LeetCode.215. 数组中的第K个最大元素     

**题目描述：**

在未排序的数组中找到第 k 个最大的元素。请注意，你需要找的是数组排序后的第 k 个最大的元素，而不是第 k 个不同的元素。

```
示例 1:

输入: [3,2,1,5,6,4] 和 k = 2
输出: 5
示例 2:

输入: [3,2,3,1,2,4,5,5,6] 和 k = 4
输出: 4
```

说明:

你可以假设 k 总是有效的，且 1 ≤ k ≤ 数组的长度。

**解答：**

方法零：排序
最朴素的方法是先对数组进行排序，再返回倒数第 k 个元素，就像 Python 中的 sorted(nums)[-k]。 算法的时间复杂度为O(NlogN)，空间复杂度为 O(1)。这个时间复杂度并不令人满意，让我们试着用额外空间来优化时间复杂度。

方法一：堆
思路是创建一个小顶堆，将所有数组中的元素加入堆中，并保持堆的大小小于等于 k。这样，堆中就保留了前 k 个最大的元素。这样，堆顶的元素就是正确答案。

像大小为 k 的堆中添加元素的时间复杂度为 O(logk)，我们将重复该操作 N 次，故总时间复杂度为O(Nlogk)。

在 Python 的 heapq 库中有一个 nlargest 方法，具有同样的时间复杂度，能将代码简化到只有一行。

本方法优化了时间复杂度，但需要 O(k) 的空间复杂度。

![image-20190712205946453](http://ww3.sinaimg.cn/large/006tNc79ly1g4xcs5c06ij311u0fuwfx.jpg)

![image-20190712210024384](http://ww4.sinaimg.cn/large/006tNc79ly1g4xcsvszg4j313g0gcjs5.jpg)

![image-20190712210105859](http://ww2.sinaimg.cn/large/006tNc79ly1g4xctml0nzj312w0eet9m.jpg)

![image-20190712210128943](http://ww3.sinaimg.cn/large/006tNc79ly1g4xcu1cy73j312y0fcjsi.jpg)

![image-20190712210147761](http://ww1.sinaimg.cn/large/006tNc79ly1g4xcudpctrj312e0hcdh7.jpg)

![image-20190712210206627](http://ww4.sinaimg.cn/large/006tNc79ly1g4xcuqh9gcj312m0hu0ua.jpg)

![image-20190712210244547](http://ww2.sinaimg.cn/large/006tNc79ly1g4xcvebaq7j31220jegnd.jpg)

![image-20190712210305782](http://ww2.sinaimg.cn/large/006tNc79ly1g4xcvxe2khj313a0jiq4w.jpg)

![image-20190712210337425](http://ww4.sinaimg.cn/large/006tNc79ly1g4xcwciuxcj311w0jqq51.jpg)



![image-20190712210544264](http://ww3.sinaimg.cn/large/006tNc79ly1g4xd1c5z2mj313i0lujwq.jpg)

![image-20190712210707961](/Users/liangjing/Library/Application Support/typora-user-images/image-20190712210707961.png)

```java
class Solution {
    public int findKthLargest(int[] nums, int k) {
        // init heap 'the smallest element first'
        PriorityQueue<Integer> heap =
            new PriorityQueue<Integer>((n1, n2) -> n1 - n2);

    // keep k largest elements in the heap
    for (int n: nums) {
      heap.add(n);
      if (heap.size() > k)
        heap.poll();
    }

    // output
    return heap.poll();        
  }
}
```


复杂度分析

时间复杂度 : O(Nlogk)。
空间复杂度 : O(k)，用于存储堆元素。 

方法二：快速选择
快速选择算法 的平均时间复杂度为 O(N)。就像快速排序那样，本算法也是 Tony Hoare 发明的，因此也被称为 Hoare选择算法。

本方法大致上与快速排序相同。简便起见，注意到第 k 个最大元素也就是第 N - k 个最小元素，因此可以用第 k 小算法来解决本问题。

首先，我们选择一个枢轴，并在线性时间内定义其在排序数组中的位置。这可以通过 划分算法 的帮助来完成。

为了实现划分，沿着数组移动，将每个元素与枢轴进行比较，并将小于枢轴的所有元素移动到枢轴的左侧。

这样，在输出的数组中，枢轴达到其合适位置。所有小于枢轴的元素都在其左侧，所有大于或等于的元素都在其右侧。

这样，数组就被分成了两部分。如果是快速排序算法，会在这里递归地对两部分进行快速排序，时间复杂度为O(NlogN)。

而在这里，由于知道要找的第 N - k 小的元素在哪部分中，我们不需要对两部分都做处理，这样就将平均时间复杂度下降到 O(N)。

最终的算法十分直接了当 :

随机选择一个枢轴。

使用划分算法将枢轴放在数组中的合适位置 pos。将小于枢轴的元素移到左边，大于等于枢轴的元素移到右边。

比较 pos 和 N - k 以决定在哪边继续递归处理。

**! 注意，本算法也适用于有重复的数组**

![image.png](http://ww4.sinaimg.cn/large/006tNc79ly1g4xd3534eqj31ag0run1m.jpg)

```java
import java.util.Random;
class Solution {
  int [] nums;

  public void swap(int a, int b) {
    int tmp = this.nums[a];
    this.nums[a] = this.nums[b];
    this.nums[b] = tmp;
  }

  public int partition(int left, int right, int pivot_index) {
    int pivot = this.nums[pivot_index];
    // 1. move pivot to end
    swap(pivot_index, right);
    int store_index = left;

// 2. move all smaller elements to the left
for (int i = left; i <= right; i++) {
  if (this.nums[i] < pivot) {
    swap(store_index, i);
    store_index++;
  }
}

// 3. move pivot to its final place
swap(store_index, right);

return store_index;

  }

  public int quickselect(int left, int right, int k_smallest) {
    /*
    Returns the k-th smallest element of list within left..right.
    */

if (left == right) // If the list contains only one element,
  return this.nums[left];  // return that element

// select a random pivot_index
Random random_num = new Random();
int pivot_index = left + random_num.nextInt(right - left); 

pivot_index = partition(left, right, pivot_index);

// the pivot is on (N - k)th smallest position
if (k_smallest == pivot_index)
  return this.nums[k_smallest];
// go left side
else if (k_smallest < pivot_index)
  return quickselect(left, pivot_index - 1, k_smallest);
// go right side
return quickselect(pivot_index + 1, right, k_smallest);

  }

  public int findKthLargest(int[] nums, int k) {
    this.nums = nums;
    int size = nums.length;
    // kth largest is (N - k)th smallest
    return quickselect(0, size - 1, size - k);
  }
}
```

复杂度分析

时间复杂度 : 平均情况 O(N)，最坏情况 O(N^2)。
空间复杂度 : O(1)。