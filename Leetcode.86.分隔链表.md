# Leetcode.86.分隔链表

**题目描述：**

给定一个链表和一个特定值 x，对链表进行分隔，使得所有小于 x 的节点都在大于或等于 x 的节点之前。

你应当保留两个分区中每个节点的初始相对位置。

示例:

```
输入: head = 1->4->3->2->5->2, x = 3
输出: 1->2->2->4->3->5
```

**题目解答：**

 * ```java
 **

- Definition for singly-linked list.

    - public class ListNode {
    
    - int val;
    
    - ListNode next;
    
    - ListNode(int x) { val = x; }
    
    - }
      */
      // 时间复杂度：O(n)
      // 空间复杂度：O(1)
      class Solution {
      public ListNode partition(ListNode head, int x) {
          
      ListNode dummyHead1 = new ListNode(0);
      ListNode dummyHead2 = new ListNode(0);
      ListNode before = dummyHead1;
      ListNode after = dummyHead2;
    
      while(head != null){
          if(head.val < x){
              before.next = head;
              // 注意顺序
              head = head.next;
          before = before.next;
           before.next = null;              
       }else{
           after.next = head;
           head = head.next;   
           after = after.next;
           after.next = null;          
       }
   }
 
   before.next = dummyHead2.next;
   return dummyHead1.next;
 
   }
 }
 ```
 
 