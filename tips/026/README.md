# [Remove Duplicates from Sorted Array][title]

## Description

Given a sorted array, remove the duplicates [**in-place**](https://en.wikipedia.org/wiki/In-place_algorithm) such that each element appear only *once* and return the new length.

Do not allocate extra space for another array, you must do this by **modifying the input array in-place** with O(1) extra memory.

**Example:**

```
Given nums = [1,1,2],

Your function should return length = 2, with the first two elements of nums being 1 and 2 respectively.
It doesn't matter what you leave beyond the new length.
```

**Tags:** Array, Two Pointers


## 思路

题意是让你从一个有序的数组中移除重复的元素，并返回之后数组的长度。我的思路是判断长度小于等于 1 的话直接返回原长度即可，否则的话遍历一遍数组，用一个 `tail` 变量指向尾部，如果后面的元素和前面的元素不同，就让 `tail` 变量加一，最后返回 `tail` 即可。
java:
```java
class Solution {
    public int removeDuplicates(int[] nums) {
        int len = nums.length;
        if (len <= 1) return len;
        int tail = 1;
        for (int i = 1; i < len; ++i) {
            if (nums[i - 1] != nums[i]) {
                nums[tail++] = nums[i];
            }
        }
        return tail;
    }
}
```
kotlin(268 ms/96.77%):
与java版思路大体一致。非要说出点不同的话,上方的java代码较为简洁;但在存在大量相等数字的时候,下方的kotlin代码运行效率更高。(详见内部的while循环)
```kotlin
class Solution {
    fun removeDuplicates(nums: IntArray): Int {
        if (nums.size < 2) return nums.size
        var t: Int
        var j = 1
        var i = 1
        while (i < nums.size) {
            t = i
            while (i < nums.size && nums[i] == nums[t - 1]) {
                i++
            }
            if (i < nums.size) {
                nums[j] = nums[i]
                j++
                i++
            }
        }
        return j
    }
}
```
javascript:
```javascript
var removeDuplicates = function(nums) {
    for (var i = 1;i < nums.length; i++) {
        for (var j = 0; j < i; j++){
            if (nums[i] === nums[j]) {
                nums.splice(i, 1)
				i = i - 1
            }
        }
    }
    return nums.length
};
```


## 结语

如果你同我们一样热爱数据结构、算法、LeetCode，可以关注我们 GitHub 上的 LeetCode 题解：[LeetCode-Solution][ls]



[title]: https://leetcode.com/problems/remove-duplicates-from-sorted-array
[ls]: https://github.com/RichCodersAndMe/LeetCode-Solution
