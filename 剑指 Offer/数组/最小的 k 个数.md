---
最小的 k 个数
---

#### 题目描述

LeetCode：https://leetcode.cn/problems/zui-xiao-de-kge-shu-lcof/

【Easy】输入整数数组 `arr` ，找出其中最小的 `k` 个数。例如，输入4、5、1、6、2、7、3、8这8个数字，则最小的4个数字是1、2、3、4。

示例：

```java
输入：arr = [3,2,1], k = 2
输出：[1,2] 或者 [2,1]
```

#### 思路

1. 先排序再取前 k 个数。
1. 大根堆。
1. 手写快排实现。
1. 快排，只要基准值的索引正好是第 k+1 个数，那么基准值的左边，就是最小的 k 个数了。
1. 既然数字是有上限的，那么直接计数排序即可。

#### 实现

思路一：

```java
    /**
     * 最小的 k 个数
     * 时间复杂度：O(nlogn)
     * 空间复杂度：O(n)
     */
    public int[] getLeastNumbers(int[] arr, int k) {
        if (arr == null || arr.length == 0 || k == 0) {
            return new int[0];
        }
        Arrays.sort(arr);
        int[] res = new int[k];
        int index = 0;
        for (int i = 0; i < k; i++) {
            res[i] = arr[index++];
        }
        return res;
    }
```

思路二：

```java
    /**
     * 最小的 k 个数
     * 时间复杂度：O(nlogk)
     * 空间复杂度：O(k)
     */
    public int[] getLeastNumbers(int[] arr, int k) {
        if (arr == null || arr.length == 0 || k == 0) {
            return new int[0];
        }
        Queue<Integer> queue = new PriorityQueue<>((a1, a2) -> a2 - a1);
        for (int i = 0; i < k; i++) {
            queue.add(arr[i]);
        }
        for (int i = k; i < arr.length; i++) {
            if (arr[i] < queue.peek()) {
                queue.poll();
                queue.add(arr[i]);
            }
        }
        int[] res = new int[k];
        int index = 0;
        while (!queue.isEmpty()) {
            res[index++] = queue.poll();
        }
        return res;
    }
```

思路三：

```java
    /**
     * 最小的 k 个数
     * 时间复杂度：O(nlogn)
     * 空间复杂度：O(logn)
     */
    public int[] getLeastNumbers(int[] arr, int k) {
        if (arr == null || arr.length == 0 || k == 0) {
            return new int[0];
        }
        quickSort(arr, 0, arr.length - 1);
        int[] res = new int[k];
        for (int i = 0; i < k; i++) {
            res[i] = arr[i];
        }
        return res;
    }

    private void quickSort(int[] arr, int left, int right) {
        if (left >= right) {
            return;
        }
        int l = left, r = right;
        while (l < r) {
            while (l < r && arr[r] >= arr[left]) {
                r--;
            }
            while (l < r && arr[l] <= arr[left]) {
                l++;
            }
            swap(arr, l, r);
        }
        swap(arr, l, left);
        quickSort(arr, left, l - 1);
        quickSort(arr, l + 1, right);
    }

    private void swap(int[] arr, int m, int n) {
        if (m == n) {
            return;
        }
        int temp = arr[m];
        arr[m] = arr[n];
        arr[n] = temp;
    }
```

思路四：

```java
    /**
     * 最小的 k 个数
     * 时间复杂度：O(n)
     * 空间复杂度：O(logn)
     */
    public int[] getLeastNumbers(int[] arr, int k) {
        if (arr == null || arr.length == 0 || k == 0) {
            return new int[0];
        }
        return quickSort(arr, 0, arr.length - 1, k);
    }

    private int[] quickSort(int[] arr, int left, int right, int k) {
        int l = left, r = right;
        while (l < r) {
            while (l < r && arr[r] >= arr[left]) {
                r--;
            }
            while (l < r && arr[l] <= arr[left]) {
                l++;
            }
            swap(arr, l, r);
        }
        swap(arr, l, left);
        if (l > k) {
            return quickSort(arr, left, l - 1, k);
        } else if (l < k) {
            return quickSort(arr, l + 1, right, k);
        }
        return Arrays.copyOf(arr, k);
    }

    private void swap(int[] arr, int m, int n) {
        if (m == n) {
            return;
        }
        int temp = arr[m];
        arr[m] = arr[n];
        arr[n] = temp;
    }
```

思路五：

```java
    /**
     * 最小的 k 个数
     * 时间复杂度：O(n)
     * 空间复杂度：O(n)
     */
    public int[] getLeastNumbers(int[] arr, int k) {
        if (arr == null || arr.length == 0 || k == 0) {
            return new int[0];
        }
        int[] temp = new int[10001];
        for (int num : arr) {
            temp[num]++;
        }
        int[] res = new int[k];
        int index = 0;
        for (int i = 0; i < temp.length; i++) {
            if (temp[i] == 0) {
                continue;
            }
            for (int j = 0; j < temp[i]; j++) {
                res[index++] = i;
                if (index == k) {
                    return res;
                }
            }
        }
        return res;
    }
```

