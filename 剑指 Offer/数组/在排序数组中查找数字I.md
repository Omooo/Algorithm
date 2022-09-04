---
在排序数组中查找数字I
---

#### 题目描述

LeetCode：https://leetcode.cn/problems/zai-pai-xu-shu-zu-zhong-cha-zhao-shu-zi-lcof/

【Easy】统计一个数字在排序数组中出现的次数。

示例：

```java
输入: nums = [5,7,7,8,8,10], target = 8
输出: 2
```

#### 思路

1. 二分查找。

#### 实现

思路一：

```java
    /**
     * 在排序数组中查找数字 I
     * 时间复杂度：O(logn)
     * 空间复杂度：O(1)
     */
    public int search(int[] nums, int target) {
        if (nums == null || nums.length == 0) {
            return 0;
        }
        int left = 0, right = nums.length - 1;
        while (left <= right) {
            int mid = left + (right - left) / 2;
            if (nums[mid] < target) {
                left = mid + 1;
            } else if (nums[mid] > target) {
                right = mid - 1;
            } else {
                if (nums[left] != target) {
                    left++;
                } else if (nums[right] != target) {
                    right--;
                } else {
                    break;
                }
            }
        }
        return right - left + 1;
    }
```

