# Leetcode.445.两数相加 II

**题目描述：**

给定两个非空链表来代表两个非负整数。数字最高位位于链表开始位置。它们的每个节点只存储单个数字。将这两数相加会返回一个新的链表。

 

你可以假设除了数字 0 之外，这两个数字都不会以零开头。

进阶:

如果输入链表不能修改该如何处理？换句话说，你不能对列表中的节点进行翻转。

示例:

```
输入: (7 -> 2 -> 4 -> 3) + (5 -> 6 -> 4)
输出: 7 -> 8 -> 0 -> 7
```

**代码解答：**

```java
/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode(int x) { val = x; }
 * }
 */
// 时间复杂度：O(max(m,n))
// 空间复杂度：O(max(m,n))
class Solution {
    public ListNode addTwoNumbers(ListNode l1, ListNode l2) {
        
        Stack<Integer> s1 = new Stack();
        Stack<Integer> s2 = new Stack();
        push(s1,l1);
        push(s2,l2);
        ListNode node = null;
        int carry = 0;
        
        while(!s1.empty() || !s2.empty()){
            int x = s1.empty() ? 0 : s1.pop();
            int y = s2.empty() ? 0 : s2.pop();
            int sum = carry + x + y;
            carry = sum / 10;
            ListNode temp = new ListNode(sum % 10);
            temp.next = node;
            node = temp;
        }
        
        if(carry > 0){
            ListNode temp = new ListNode(1);
            temp.next = node;
            node = temp;
        }
        
        return node;
    }
    
    private void push(Stack s , ListNode head){
        
        while(head != null){
            s.push(head.val);
            head = head.next;
        }
    }
}
```

