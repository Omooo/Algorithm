---
链表中倒数第 k 个节点
---

#### 题目描述

LeetCode：https://leetcode.cn/problems/lian-biao-zhong-dao-shu-di-kge-jie-dian-lcof/

【Easy】输入一个链表，输出该链表中倒数第 k 个节点。为了符合大多数人的习惯，本题从 1 开始计数，即链表的尾节点是倒数第 1 个节点。

【示例】链表：1->2->3->4->5 和 k = 2。返回：4->5。

#### 思路

1. 快慢指针，快指针先走 k 步，然后一起走。

#### 实现

思路一：

```java
    /**
     * 时间复杂度: O(n)
     * 空间复杂度: O(1)
     */
    public ListNode getKthFromEnd(ListNode head, int k) {
        if (head == null) {
            return null;
        }
        ListNode temp = new ListNode();
        temp.next = head;
        ListNode fast = head;
        for (int i = 0; i < k; i++) {
            fast = fast.next;
        }
        while (fast != null) {
            fast = fast.next;
            temp = temp.next;
        }
        return temp.next;
    }
```

