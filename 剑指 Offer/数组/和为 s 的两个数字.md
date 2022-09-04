---
和为 s 的两个数字
---

#### 题目描述

LeetCode：https://leetcode.cn/problems/he-wei-sde-liang-ge-shu-zi-lcof/

【Easy】输入一个递增排序的数组和一个数字 s，在数组中查找两个数，使得它们的和正好是 s。如果有多对数字的和等于 s，则输出任意一对即可。

示例：

```java
输入：nums = [2,7,11,15], target = 9
输出：[2,7] 或者 [7,2]
```

#### 思路

1. 双指针。

#### 实现

思路一：

```java
    /**
     * 和为 s 的两个数字
     * 时间复杂度: O(n)
     * 空间复杂度: O(1)
     */
    public int[] twoSum(int[] nums, int target) {
        if (nums == null || nums.length == 0) {
            return new int[2];
        }
        int left = 0, right = nums.length - 1;
        while (left < right) {
            int sum = nums[left] + nums[right];
            if (sum == target) {
                return new int[]{nums[left], nums[right]};
            } else if (sum < target) {
                left++;
            } else {
                right--;
            }
        }
        return new int[2];
    }
```
