# Leetcode.149. 直线上最多的点数

**题目描述：**

给定一个二维平面，平面上有 n 个点，求最多有多少个点在同一条直线上。

示例 1:

```
输入: [[1,1],[2,2],[3,3]]
输出: 3
解释:
^
|
|        o
|     o
|  o  
+------------->
0  1  2  3  4
```


示例 2:

```
输入: [[1,1],[3,2],[5,3],[4,1],[2,3],[1,4]]
输出: 4
解释:
^
|
|  o
|     o        o
|        o
|  o        o
+------------------->
0  1  2  3  4  5  6
```

**方法 ：枚举**
首先简化这个问题：找出一条通过点 i 的直线，使得经过最多的点。

我们会发现，其实只需要考虑当前点之后出现的点 i + 1 .. N - 1 即可，因为通过点 i-2 的直线已经在搜索点 i-2 的过程中考虑过了。

思路非常简单：画一条通过点 i 和之后出现的点的直线，在哈希表中存储这条边并计数为 2 = 当前这条直线上有两个点。

假设现在 i < i + k < i + l 这三个点在同一条直线上，当画出一条通过 i 和 i+l 的直线会发现已经记录过了，因此对更新这条边对应的计数：count++。

如何存储一条边？

如果这条线是水平的，例如 y=c，我们可以利用常数 c 作为水平直线的哈希表的键。

注意到这里所有直线都是通过同一个点 i 的，因此并不需要记录 c 的值而只需要统计水平直线的个数。

剩下的直线可以被表示成 x = slope * y + c，同样 c 也是不需要的，因为所有直线都通过同一个点 i 所以只需要用 slope 作为直线的键。

![image-20190726230421070](http://ww3.sinaimg.cn/large/006tNc79ly1g5dn24njnpj30rw09igmj.jpg)

**代码解答：**	

```java
// 时间复杂度：O(n^2)
// 空间复杂度：O(n)
class Solution {    

public int maxPoints(int[][] points) {
    
    if(points.length == 0)
        return 0;
    
    if(points.length == 1)
        return 1;        
    
    Point[] point = new Point[points.length];
    Map<Double,Integer> map = new HashMap<>();
    int result = 0;
    int count = 0;
    
    for(int i= 0 ; i < points.length ; i++){
        int x = points[i][0];
        int y = points[i][1];
        point[i] = new Point(x,y);          
    }
    
    for(int i = 0 ; i < point.length - 1 ; i++){
        Point a = point[i];
        int temp = 0;
        for(int j = i + 1 ; j < point.length ; j++){
            Point b = point[j];                
            if(a.x == b.x && a.y == b.y){
                temp++;
            }else if(a.x == b.x){
                if(!map.containsKey(0.0))
                    map.put(0.0,1);
                else
                    map.put(0.0,map.get(0.0) + 1);
                count = map.get(0.0) > count ? map.get(0.0) : count;
            }else if(a.y == b.y){
                if(!map.containsKey(1.0 * a.y))
                    map.put(1.0 * a.y,1);
                else
                    map.put(1.0 * a.y,map.get(1.0 * a.y) + 1);
                count = map.get(1.0 * a.y) > count ? map.get(1.0 * a.y) : count;
            }else{
                double slope = getSlope(a,b);
                if(!map.containsKey(slope))
                   map.put(slope,1);
                else
                    map.put(slope,map.get(slope) + 1);
                count = (map.get(slope) > count) ? map.get(slope) : count;
            }
        }
        result = result > (count + temp + 1) ? result : (count + temp + 1);
        temp = 0;
        count = 0;
        map.clear();
    }
    return result;
}

// 获取两点间的斜率
private double getSlope(Point a , Point b){
    double slope = 1.0 * (b.x - a.x) / (b.y - a.y) + 0.0;
    return slope;
}

}

public class Point{
    int x;
    int y;
    public Point(int x , int y){
        this.x = x;
        this.y = y;
    }
}
```