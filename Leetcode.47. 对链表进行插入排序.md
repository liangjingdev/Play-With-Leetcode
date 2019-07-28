# Leetcode.47. 对链表进行插入排序

**题目描述：**

对链表进行插入排序。

插入排序的动画演示如上。从第一个元素开始，该链表可以被认为已经部分排序（用黑色表示）。
每次迭代时，从输入数据中移除一个元素（用红色表示），并原地将其插入到已排好序的链表中。

插入排序算法：

插入排序是迭代的，每次只移动一个元素，直到所有元素可以形成一个有序的输出列表。
每次迭代中，插入排序只从输入数据中移除一个待排序的元素，找到它在序列中适当的位置，并将其插入。
重复直到所有输入数据插入完为止。

**题目解答：**

```java
/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode(int x) { val = x; }
 * }
 */
// 时间复杂度：O(n^2)
class Solution {
    public ListNode insertionSortList(ListNode head) {
        
        if(head == null || head.next == null)
            return head;
        
        ListNode dummyHead = new ListNode(0);
        dummyHead.next = head;
        ListNode cur = head;
        
        while(cur.next != null){
            
            if(cur.next.val < cur.val){
                ListNode op = cur.next;
                cur.next = cur.next.next;
                ListNode start = dummyHead;
                while(start.next != null){
                    if(op.val < start.next.val){
                        op.next = start.next;
                        start.next = op;
                        break;
                    }else{
                        start = start.next;
                    }
                }
            }else{
                cur = cur.next;
            }
        }
        return dummyHead.next;
    }
}
```