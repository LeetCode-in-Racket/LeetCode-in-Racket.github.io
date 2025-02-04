[![](https://img.shields.io/github/stars/LeetCode-in-Racket/LeetCode-in-Racket?label=Stars&style=flat-square)](https://github.com/LeetCode-in-Racket/LeetCode-in-Racket)
[![](https://img.shields.io/github/forks/LeetCode-in-Racket/LeetCode-in-Racket?label=Fork%20me%20on%20GitHub%20&style=flat-square)](https://github.com/LeetCode-in-Racket/LeetCode-in-Racket/fork)

## 46\. Permutations

Medium

Given an array `nums` of distinct integers, return _all the possible permutations_. You can return the answer in **any order**.

**Example 1:**

**Input:** nums = [1,2,3]

**Output:** [[1,2,3],[1,3,2],[2,1,3],[2,3,1],[3,1,2],[3,2,1]]

**Example 2:**

**Input:** nums = [0,1]

**Output:** [[0,1],[1,0]]

**Example 3:**

**Input:** nums = [1]

**Output:** [[1]]

**Constraints:**

*   `1 <= nums.length <= 6`
*   `-10 <= nums[i] <= 10`
*   All the integers of `nums` are **unique**.

## Solution

```racket
; #Medium #Top_100_Liked_Questions #Top_Interview_Questions #Array #Backtracking
; #Algorithm_I_Day_11_Recursion_Backtracking #Level_2_Day_20_Brute_Force/Backtracking
; #Udemy_Backtracking/Recursion #Top_Interview_150_Backtracking #Big_O_Time_O(n*n!)_Space_O(n+n!)
; #2025_02_03_Time_0_(100.00%)_Space_101.43_(66.67%)

(define/contract (permute nums)
  (-> (listof exact-integer?) (listof (listof exact-integer?)))
  (cond [(empty? nums) (list empty)]
        [else (for/fold ([l empty])([i nums])
    (append (map (lambda (lst) (cons i lst)) (permute (remove i nums))) l)
    )
  ]))
```