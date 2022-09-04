---
删除链表的倒数第 n 个节点
---

#### 每日一汤

失之东隅，收之桑榆。

你在某处，有所失，在另一处，终有所得。

#### 题目描述

LeetCode：https://leetcode.cn/problems/SLwz0R/

【Medium】给定一个链表，删除链表的倒数第 n 个节点，并且返回链表的头节点。

```java
输入：head = [1,2,3,4,5], n = 2
输出：[1,2,3,5]
```

#### 思路

1. 求链表长度，找到删除节点的前序节点。
2. 双指针。
3. 使用栈。

#### 实现

思路一：

```java
    /**
     * 时间复杂度: O(n)
     * 空间复杂度: O(1)
     */
    public ListNode removeNthFromEnd(ListNode head, int n) {
        if (head == null) {
            return null;
        }
        int length = 0;
        ListNode temp = head;
        while (temp != null) {
            length++;
            temp = temp.next;
        }
        ListNode h1 = new ListNode();
        h1.next = head;
        ListNode h2 = h1;
        for (int i = 0; i < length - n; i++) {
            h2 = h2.next;
        }
        h2.next = h2.next.next;
        return h1.next;
    }
```

思路二：

```java
    /**
     * 时间复杂度: O(n)
     * 空间复杂度: O(1)
     */
    public ListNode removeNthFromEnd(ListNode head, int n) {
        if (head == null) {
            return null;
        }
        ListNode temp = new ListNode();
        temp.next = head;
        ListNode h1 = temp;
        ListNode h2 = head;
        for (int i = 0; i < n; i++) {
            h2 = h2.next;
        }
        while (h2 != null) {
            h2 = h2.next;
            h1 = h1.next;
        }
        if (h1 != null && h1.next != null) {
            h1.next = h1.next.next;
        }
        return temp.next;
    }
```

思路三：

```java
    /**
     * 时间复杂度: O(n)
     * 空间复杂度: O(n)
     */
    public ListNode removeNthFromEnd(ListNode head, int n) {
        if (head == null) {
            return null;
        }
        ListNode temp = new ListNode(0, head);
        ListNode cur = temp;
        Stack<ListNode> stack = new Stack<>();
        while (cur != null) {
            stack.push(cur);
            cur = cur.next;
        }
        for (int i = 0; i < n; i++) {
            stack.pop();
        }
        ListNode pre = stack.peek();
        pre.next = pre.next.next;
        return temp.next;
    }
```

