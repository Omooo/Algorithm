---
二叉搜索树的第 k 大节点
---

#### 题目描述

LeetCode：https://leetcode.cn/problems/er-cha-sou-suo-shu-de-di-kda-jie-dian-lcof/

【Easy】输入一棵二叉搜索树，请找出其中第 k 大的节点的值。

示例：

```java
输入: root = [3,1,4,null,2], k = 1
   3
  / \
 1   4
  \
   2
输出: 4
```

#### 思路

1. 中序遍历生成 list，然后直接取对应索引的值即可。
2. 计算右子树的节点个数，右子树的节点个数 + 1 就是根节点的第 k 大数字。
3. 中序遍历的逆序，第 k 大元素就是递归了第 k 次。

#### 实现

思路一：

```java
    /**
     * 二叉搜索树的第 k 大节点
     * 时间复杂度：O(n)
     * 空间复杂度：O(n)
     */
    public int kthLargest(TreeNode root, int k) {
        if (root == null) {
            return -1;
        }
        List<Integer> list = new ArrayList<>();
        dfs(root, list);
        return list.get(list.size() - k);
    }

    private void dfs(TreeNode root, List<Integer> list) {
        if (root == null) {
            return;
        }
        dfs(root.left, list);
        list.add(root.val);
        dfs(root.right, list);
    }
```

思路二：

```java
    /**
     * 二叉搜索树的第 k 大节点
     * 时间复杂度：O(n)
     * 空间复杂度：O(n)
     */
    public int kthLargest(TreeNode root, int k) {
        if (root == null) {
            return -1;
        }
        int rightCount = count(root.right);
        if (rightCount + 1 == k) {
            return root.val;
        } else if (rightCount + 1 > k) {
            return kthLargest(root.right, k);
        }
        return kthLargest(root.left, k - rightCount - 1);
    }

    private int count(TreeNode root) {
        if (root == null) {
            return 0;
        }
        return count(root.left) + count(root.right) + 1;
    }
```

思路三：

```java
    /**
     * 二叉搜索树的第 k 大节点
     * 时间复杂度：O(n)
     * 空间复杂度：O(n)
     */
    private int count = 0, res = -1;

    public int kthLargest(TreeNode root, int k) {
        if (root == null) {
            return -1;
        }
        dfs(root, k);
        return res;
    }

    private void dfs(TreeNode root, int k) {
        if (root == null) {
            return;
        }
        dfs(root.right, k);
        if (++count == k) {
            res = root.val;
            return;
        }
        dfs(root.left, k);
    }
```

