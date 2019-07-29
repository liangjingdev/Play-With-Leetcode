# Leetcode.148. 排序链表

**题目描述：**

在 O(n log n) 时间复杂度和常数级空间复杂度下，对链表进行排序。

示例 1:

```
输入: 4->2->1->3
输出: 1->2->3->4
```


示例 2:

```
输入: -1->5->3->4->0
输出: -1->0->3->4->5
```

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
// 时间复杂度：O(nlogn)
class Solution {
    public ListNode sortList(ListNode head) {
        if(head == null || head.next == null)
            return head;
        ListNode[] array = new ListNode[64];
        ListNode dummyHead = new ListNode(0);
        ListNode iter = dummyHead;
        int maxIndex = 0;
        while(head != null){
            ListNode cur = new ListNode(head.val);
            int i = 0;
            ListNode newListNode = cur;
            while(array[i] != null){
                newListNode = mergeTwoSortedLinkedList(newListNode,array[i]);
                array[i] = null;
                i++;
            }
            array[i] = newListNode;
            if(i >= maxIndex)
                maxIndex = i;
            i = 0;
            head = head.next;
        }
        
        for(int i = 0 ; i <= maxIndex ; i++){
            if(array[i] != null)
                iter.next = mergeTwoSortedLinkedList(iter.next,array[i]);
        }
        
        return dummyHead.next;
    }
    
    private ListNode mergeTwoSortedLinkedList(ListNode l1 , ListNode l2){
        ListNode dummyHead = new ListNode(0);
        ListNode iter = dummyHead;
        while(l1 != null && l2 != null){
            if(l1.val <= l2.val){
                iter.next = l1;
                l1 = l1.next;         
            }else{
                iter.next = l2;
                l2 = l2.next;
            }
            iter = iter.next;
        }
        if(l1 == null) iter.next = l2;
        if(l2 == null) iter.next = l1;
        return dummyHead.next;
    } 
}
```

