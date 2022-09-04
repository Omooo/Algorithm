---
合并 K 个有序链表
---

#### 每日一汤

莫道桑榆晚，为霞尚满天。

有的事迟一点，慢一点都没有关系。因为你要相信，一切都是最好的安排。

#### 题目描述

LeetCode：https://leetcode.cn/problems/vvXgSW/

【Hard】给定一个链表数组，每个链表都是按照升序排列的，合并这 K 个链表返回合并后的头节点。

```java
输入：lists = [[1,4,5],[1,3,4],[2,6]]
输出：[1,1,2,3,4,4,5,6]
```

#### 思路

1. 两两合并链表。
2. 归并合并，可以使用递归和非递归写法。

#### 实现

思路一：

```javascript
    /**
     * 合并 K 个有序链表
     * 时间复杂度: O(n*k^2)
     * 空间复杂度: O(1)
     */
    public ListNode mergeKLists(ListNode[] lists) {
        if (lists == null || lists.length == 0) {
            return null;
        }
        ListNode head = null;
        for (ListNode node : lists) {
            head = merge(head, node);
        }
        return head;
    }

    /**
     * 合并两个有序链表
     */
    private ListNode merge(ListNode l1, ListNode l2) {
        if (l1 == null) {
            return l2;
        }
        if (l2 == null) {
            return l1;
        }
        ListNode head = new ListNode();
        ListNode temp = head;
        while (l1 != null && l2 != null) {
            if (l1.val < l2.val) {
                temp.next = l1;
                l1 = l1.next;
            } else {
                temp.next = l2;
                l2 = l2.next;
            }
            temp = temp.next;
        }
        temp.next = l1 == null ? l2 : l1;
        return head.next;
    }
```

思路二：

```java
    /**
     * 合并 K 个有序链表（递归写法）
     * 时间复杂度: O(nk*logk)
     * 空间复杂度: O(logk)
     */
    public ListNode mergeKLists(ListNode[] lists) {
        return mergeKLists(lists, 0, lists.length - 1);
    }

    public ListNode mergeKLists(ListNode[] lists, int left, int right) {
        if (left == right) {
            return lists[left];
        }
        if (left > right) {
            return null;
        }
        int mid = (left + right) / 2;
        ListNode l1 = mergeKLists(lists, left, mid);
        ListNode l2 = mergeKLists(lists, mid + 1, right);
        return merge(l1, l2);
    }

    /**
     * 合并两个有序链表
     */
    private ListNode merge(ListNode l1, ListNode l2) {
        if (l1 == null) {
            return l2;
        }
        if (l2 == null) {
            return l1;
        }
        ListNode head = new ListNode();
        ListNode temp = head;
        while (l1 != null && l2 != null) {
            if (l1.val < l2.val) {
                temp.next = l1;
                l1 = l1.next;
            } else {
                temp.next = l2;
                l2 = l2.next;
            }
            temp = temp.next;
        }
        temp.next = l1 == null ? l2 : l1;
        return head.next;
    }
```

思路三：

```java
    /**
     * 合并 K 个有序链表（非递归写法）
     * 时间复杂度: O(nk)
     * 空间复杂度: O(1)
     */
    public ListNode mergeKLists(ListNode[] lists) {
        if (lists == null || lists.length == 0) {
            return null;
        }
        ListNode head = null;
        int count = lists.length - 1;
        int dis = 2;
        while (count > 0) {
            for (int i = 0, j = dis / 2; j < lists.length; i = i + dis, j = j + dis) {
                lists[i] = merge(lists[i], lists[j]);
                count--;
            }
            dis = dis * 2;
        }
        return lists[0];
    }

    /**
     * 合并两个有序链表
     */
    private ListNode merge(ListNode l1, ListNode l2) {
        if (l1 == null) {
            return l2;
        }
        if (l2 == null) {
            return l1;
        }
        ListNode head = new ListNode();
        ListNode temp = head;
        while (l1 != null && l2 != null) {
            if (l1.val < l2.val) {
                temp.next = l1;
                l1 = l1.next;
            } else {
                temp.next = l2;
                l2 = l2.next;
            }
            temp = temp.next;
        }
        temp.next = l1 == null ? l2 : l1;
        return head.next;
    }
```

