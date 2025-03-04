[![](https://img.shields.io/github/stars/LeetCode-in-Racket/LeetCode-in-Racket?label=Stars&style=flat-square)](https://github.com/LeetCode-in-Racket/LeetCode-in-Racket)
[![](https://img.shields.io/github/forks/LeetCode-in-Racket/LeetCode-in-Racket?label=Fork%20me%20on%20GitHub%20&style=flat-square)](https://github.com/LeetCode-in-Racket/LeetCode-in-Racket/fork)

## 198\. House Robber

Medium

You are a professional robber planning to rob houses along a street. Each house has a certain amount of money stashed, the only constraint stopping you from robbing each of them is that adjacent houses have security systems connected and **it will automatically contact the police if two adjacent houses were broken into on the same night**.

Given an integer array `nums` representing the amount of money of each house, return _the maximum amount of money you can rob tonight **without alerting the police**_.

**Example 1:**

**Input:** nums = [1,2,3,1]

**Output:** 4

**Explanation:** Rob house 1 (money = 1) and then rob house 3 (money = 3). Total amount you can rob = 1 + 3 = 4.

**Example 2:**

**Input:** nums = [2,7,9,3,1]

**Output:** 12

**Explanation:** Rob house 1 (money = 2), rob house 3 (money = 9) and rob house 5 (money = 1). Total amount you can rob = 2 + 9 + 1 = 12.

**Constraints:**

*   `1 <= nums.length <= 100`
*   `0 <= nums[i] <= 400`

## Solution

```racket
(define/contract (rob nums)
  (-> (listof exact-integer?) exact-integer?)
  (let ([n (length nums)])
    (cond [(= n 1) (first nums)]
          [(= n 2) (max (first nums) (second nums))]
          [(= n 3) (max (+ (first nums) (third nums)) (second nums))]
          [else
           (let-values ([(a b c d)
           (for/fold ([dp0 (first nums)]
                      [dp1 (max (first nums) (second nums))]
                      [dp2 (max (+ (first nums) (third nums)) (second nums))]
                      [prev-elem (third nums)])
            ([i (cdddr nums)])
             (values dp1 dp2 (max (+ i dp1) (+ prev-elem dp0)) i))])
             c)
  ])))
```