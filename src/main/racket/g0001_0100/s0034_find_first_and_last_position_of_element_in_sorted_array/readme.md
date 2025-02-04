[![](https://img.shields.io/github/stars/LeetCode-in-Racket/LeetCode-in-Racket?label=Stars&style=flat-square)](https://github.com/LeetCode-in-Racket/LeetCode-in-Racket)
[![](https://img.shields.io/github/forks/LeetCode-in-Racket/LeetCode-in-Racket?label=Fork%20me%20on%20GitHub%20&style=flat-square)](https://github.com/LeetCode-in-Racket/LeetCode-in-Racket/fork)

## 34\. Find First and Last Position of Element in Sorted Array

Medium

Given an array of integers `nums` sorted in non-decreasing order, find the starting and ending position of a given `target` value.

If `target` is not found in the array, return `[-1, -1]`.

You must write an algorithm with `O(log n)` runtime complexity.

**Example 1:**

**Input:** nums = [5,7,7,8,8,10], target = 8

**Output:** [3,4]

**Example 2:**

**Input:** nums = [5,7,7,8,8,10], target = 6

**Output:** [-1,-1]

**Example 3:**

**Input:** nums = [], target = 0

**Output:** [-1,-1]

**Constraints:**

*   <code>0 <= nums.length <= 10<sup>5</sup></code>
*   <code>-10<sup>9</sup> <= nums[i] <= 10<sup>9</sup></code>
*   `nums` is a non-decreasing array.
*   <code>-10<sup>9</sup> <= target <= 10<sup>9</sup></code>

## Solution

```racket
; #Medium #Top_100_Liked_Questions #Top_Interview_Questions #Array #Binary_Search
; #Algorithm_II_Day_1_Binary_Search #Binary_Search_I_Day_5 #Top_Interview_150_Binary_Search
; #Big_O_Time_O(log_n)_Space_O(1) #2025_02_03_Time_0_(100.00%)_Space_101.71_(66.67%)

(define (find-bound vec target first-val)
  (define (ptr-narrow left right)
    (let* ([mid (quotient (+ left right) 2)]
           [mid-val (vector-ref vec mid)])
      (cond [(> left right) -1]
            [(= target mid-val) (if first-val
                                    (if (or (= mid left)
                                            (< (vector-ref vec (sub1 mid)) target))
                                        mid
                                        (ptr-narrow left (sub1 right)))
                                    (if (or (= mid right)
                                            (> (vector-ref vec (add1 mid)) target))
                                        mid
                                        (ptr-narrow (add1 left) right)))]
            [(> mid-val target) (ptr-narrow left (sub1 mid))]
            [else (ptr-narrow (add1 mid) right)])))
  (ptr-narrow 0 (sub1 (vector-length vec))))


(define (search-range nums target)
  (if (empty? nums)
      '(-1 -1)
      (let* ([nums (list->vector nums)]
             [fst-val (find-bound nums target #t)])
        (if (= fst-val -1)
            '(-1 -1)
            (list fst-val
                  (find-bound nums target #f))))))
```