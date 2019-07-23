# LeetCode.15. 三数之和

**题目描述：**

给定一个包含 n 个整数的数组 nums，判断 nums 中是否存在三个元素 a，b，c ，使得 a + b + c = 0 ？找出所有满足条件且不重复的三元组。

注意：答案中不可以包含重复的三元组。

```
例如, 给定数组 nums = [-1, 0, 1, 2, -1, -4]，

满足要求的三元组集合为：
[
  [-1, 0, 1],
  [-1, -1, 2]
]
```

**题目解答：**

```java
// 时间复杂度：O(n^2)
// 空间复杂度：O(n)
class Solution {
    public List<List<Integer>> threeSum(int[] nums) {        

    if(nums == null || nums.length < 3)
        return new ArrayList<>();
    
    Set<Integer> set = new HashSet<>();
    Map<Integer,Integer> counter = new HashMap<>();
    List<List<Integer>> result = new ArrayList<>(); 
    int[] newNums = new int[nums.length];
    int k = 0;
    
    for(int i = 0 ; i < nums.length ; i++){
        int temp = nums[i];
        if(!counter.containsKey(temp))
            counter.put(temp,1);
        else
            counter.put(temp,counter.get(temp) + 1);
        set.add(temp);
    }
    
    Iterator iter = set.iterator();
    while(iter.hasNext())
        newNums[k++] = (int)iter.next();        
    
    if(counter.containsKey(0) && counter.get(0) >= 3){
        List<Integer> list = new ArrayList<>();
        list.add(0);
        list.add(0);
        list.add(0);
        result.add(list);
    }
    
    set.clear(); 
    
    for(int i = 0 ; i < k ; i++){
        for(int j = i+1 ; j < k ; j++){
            int temp = 0 - newNums[i] - newNums[j];
            List<Integer> list = new ArrayList<>();
             if(newNums[i] * 2 + newNums[j] == 0 && counter.get(newNums[i]) >= 2){
                 list.add(newNums[i]);
                 list.add(newNums[j]);
                 list.add(temp);
                 result.add(list);
             }
                
            if(newNums[i] + newNums[j] * 2 == 0 && counter.get(newNums[j]) >= 2){
                list.add(newNums[i]);
                list.add(newNums[j]);
                list.add(temp);
                result.add(list);
            }
            
           if(set.contains(temp)){   
               list.add(newNums[i]);
               list.add(newNums[j]);
               list.add(temp);
               result.add(list);
           }else
               set.add(newNums[j]);
        }
        set.clear();
    }
    return result;
  }

}
```