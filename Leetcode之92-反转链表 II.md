# Leetcode之92-反转链表 II

**题目描述：**

反转从位置 m 到 n 的链表。请使用一趟扫描完成反转。

说明:
1 ≤ m ≤ n ≤ 链表长度。

示例:

```
输入: 1->2->3->4->5->NULL, m = 2, n = 4
输出: 1->4->3->2->5->NULL
```

**代码解答：**

 * ```java
 /**

- Definition for singly-linked list.

    - public class ListNode {
    
    - int val;
    
    - ListNode next;
    
    - ListNode(int x) { val = x; }
    
    - }
      */
      // 时间复杂度：O(N)
      // 空间复杂度：O(1)
      class Solution {
      public ListNode reverseBetween(ListNode head, int m, int n) {
        
      if(head == null || head.next == null || m == n)
          return head;
    
      ListNode dummyHead = new ListNode(0);
      dummyHead.next = head;
      ListNode pre = dummyHead;
      ListNode cur = head;
      ListNode next;
      ListNode con = pre;
      ListNode tail = cur;
    
      while(m > 1){            
          pre = pre.next;
          cur = cur.next;
          con = pre;
          tail = cur;
          m--;
          n--;
      } 
    
  while(n > 0){
       next = cur.next;
       cur.next = pre;
       pre = cur;
       cur = next;
       n--;
   }
 
   con.next = pre;
   tail.next = cur;
 
   return dummyHead.next;
 
   }
 }
 ```