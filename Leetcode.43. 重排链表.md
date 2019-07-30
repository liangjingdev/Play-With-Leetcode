# Leetcode.43. 重排链表

给定一个单链表 L：L0→L1→…→Ln-1→Ln ，

将其重新排列后变为： L0→Ln→L1→Ln-1→L2→Ln-2→…

你不能只是单纯的改变节点内部的值，而是需要实际的进行节点交换。

示例 1:

```
给定链表 1->2->3->4, 重新排列为 1->4->2->3. 
```

示例 2:

```
给定链表 1->2->3->4->5, 重新排列为 1->5->2->4->3. 
```

这道题可谓是集合了各种的链表操作，把这道题的每个步骤都理解清楚了之后，链表相关的大部分题应该都可以搞定了。建议在脑中多过两遍这个题 可以把本题分为3个步骤：

1、使用双指针将链表分成两段

2、将链表后半段进行翻转

3、将两段链表进行合并

**题目解答：**

```java
/** 

\* Definition for singly-linked list. 

\* public class ListNode { 

\*     int val; 

\*     ListNode next; 

\*     ListNode(int x) { val = x; } 

\* } 

*/ 

class Solution { 

​    public void reorderList(ListNode head) { 

​        if (head == null || head.next == null) return; 

​         

​        ListNode p1 = head; 

​        ListNode p2 = head; 

​         

​        // 找到链表的一半 

​        while (p2.next != null && p2.next.next != null) { 

​            p1 = p1.next; 

​            p2 = p2.next.next; 

​        } 

​         

​        // 将链表分为两段 

​        p2 = p1.next; 

​        p1.next = null; 

​        p1 = head; 

​         

​        p2 = reverse(p2); 

​         

​        // 两条链表进行合并 

​        ListNode next1; 

​        ListNode next2; 

​        while (p2 != null) { 

​            next1 = p1.next; 

​            next2 = p2.next; 

​             

​            p1.next = p2; 

​            p2.next = next1; 

​             

​            p1 = next1; 

​            p2 = next2; 

​        } 

​    } 

​     

​    // 翻转链表 

​    private ListNode reverse(ListNode oldListNode){ 

​        if(oldListNode == null || oldListNode.next == null) 

​            return oldListNode; 

​        ListNode pre = null; 

​        ListNode cur = oldListNode; 

​        ListNode next; 

​        while(oldListNode != null){ 

​            next = oldListNode.next; 

​            oldListNode.next= pre; 

​            pre = oldListNode; 

​            oldListNode = next; 

​        } 

​        return pre; 

​    } 

} 
```