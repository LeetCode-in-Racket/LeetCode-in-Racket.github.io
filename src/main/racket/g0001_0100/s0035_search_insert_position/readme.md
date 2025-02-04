[![](https://img.shields.io/github/stars/LeetCode-in-Racket/LeetCode-in-Racket?label=Stars&style=flat-square)](https://github.com/LeetCode-in-Racket/LeetCode-in-Racket)
[![](https://img.shields.io/github/forks/LeetCode-in-Racket/LeetCode-in-Racket?label=Fork%20me%20on%20GitHub%20&style=flat-square)](https://github.com/LeetCode-in-Racket/LeetCode-in-Racket/fork)

## 35\. Search Insert Position

Easy

Given a sorted array of distinct integers and a target value, return the index if the target is found. If not, return the index where it would be if it were inserted in order.

You must write an algorithm with `O(log n)` runtime complexity.

**Example 1:**

**Input:** nums = [1,3,5,6], target = 5

**Output:** 2

**Example 2:**

**Input:** nums = [1,3,5,6], target = 2

**Output:** 1

**Example 3:**

**Input:** nums = [1,3,5,6], target = 7

**Output:** 4

**Example 4:**

**Input:** nums = [1,3,5,6], target = 0

**Output:** 0

**Example 5:**

**Input:** nums = [1], target = 0

**Output:** 0

**Constraints:**

*   <code>1 <= nums.length <= 10<sup>4</sup></code>
*   <code>-10<sup>4</sup> <= nums[i] <= 10<sup>4</sup></code>
*   `nums` contains **distinct** values sorted in **ascending** order.
*   <code>-10<sup>4</sup> <= target <= 10<sup>4</sup></code>

## Solution

```racket
; #Easy #Top_100_Liked_Questions #Array #Binary_Search #Algorithm_I_Day_1_Binary_Search
; #Binary_Search_I_Day_2 #Top_Interview_150_Binary_Search #Big_O_Time_O(log_n)_Space_O(1)
; #2025_02_03_Time_0_(100.00%)_Space_102.38_(_%)

(define (search-insert nums target [low 0] [high (sub1 (length nums))])
(if (< high low)
    low
    (let ([mid (floor (/ (+ low high) 2))])
    (if (>= (list-ref nums mid) target)
        (search-insert nums target low (sub1 mid))
        (search-insert nums target (add1 mid) high)))))
```