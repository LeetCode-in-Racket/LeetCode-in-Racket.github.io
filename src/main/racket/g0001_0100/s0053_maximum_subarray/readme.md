[![](https://img.shields.io/github/stars/LeetCode-in-Racket/LeetCode-in-Racket?label=Stars&style=flat-square)](https://github.com/LeetCode-in-Racket/LeetCode-in-Racket)
[![](https://img.shields.io/github/forks/LeetCode-in-Racket/LeetCode-in-Racket?label=Fork%20me%20on%20GitHub%20&style=flat-square)](https://github.com/LeetCode-in-Racket/LeetCode-in-Racket/fork)

## 53\. Maximum Subarray

Medium

Given an integer array `nums`, find the contiguous subarray (containing at least one number) which has the largest sum and return _its sum_.

A **subarray** is a **contiguous** part of an array.

**Example 1:**

**Input:** nums = [-2,1,-3,4,-1,2,1,-5,4]

**Output:** 6

**Explanation:** [4,-1,2,1] has the largest sum = 6.

**Example 2:**

**Input:** nums = [1]

**Output:** 1

**Example 3:**

**Input:** nums = [5,4,-1,7,8]

**Output:** 23

**Constraints:**

*   <code>1 <= nums.length <= 10<sup>5</sup></code>
*   <code>-10<sup>4</sup> <= nums[i] <= 10<sup>4</sup></code>

**Follow up:** If you have figured out the `O(n)` solution, try coding another solution using the **divide and conquer** approach, which is more subtle.

## Solution

```racket
; #Medium #Top_100_Liked_Questions #Top_Interview_Questions #Array #Dynamic_Programming
; #Divide_and_Conquer #Data_Structure_I_Day_1_Array #Dynamic_Programming_I_Day_5
; #Udemy_Famous_Algorithm #Top_Interview_150_Kadane's_Algorithm #Big_O_Time_O(n)_Space_O(1)
; #2025_02_03_Time_51_(100.00%)_Space_140.95_(100.00%)

(define/contract (recur nums)
    (-> (listof exact-integer?) pair?)
    (if (empty? nums) (cons 0 -1000000)
    (let* ([i (first nums)]
           [res (recur (cdr nums))]
           [currBest (car res)]
           [bestSofar (cdr res)]
           [currNew (max i (+ currBest i))]
           )
        (cons currNew (max bestSofar currNew)))))

(define/contract (max-sub-array nums)
  (-> (listof exact-integer?) exact-integer?)
  (cdr (recur nums)))
```