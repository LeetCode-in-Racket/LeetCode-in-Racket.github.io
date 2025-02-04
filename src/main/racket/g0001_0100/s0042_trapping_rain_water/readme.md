[![](https://img.shields.io/github/stars/LeetCode-in-Racket/LeetCode-in-Racket?label=Stars&style=flat-square)](https://github.com/LeetCode-in-Racket/LeetCode-in-Racket)
[![](https://img.shields.io/github/forks/LeetCode-in-Racket/LeetCode-in-Racket?label=Fork%20me%20on%20GitHub%20&style=flat-square)](https://github.com/LeetCode-in-Racket/LeetCode-in-Racket/fork)

## 42\. Trapping Rain Water

Hard

Given `n` non-negative integers representing an elevation map where the width of each bar is `1`, compute how much water it can trap after raining.

**Example 1:**

![](https://assets.leetcode.com/uploads/2018/10/22/rainwatertrap.png)

**Input:** height = [0,1,0,2,1,0,1,3,2,1,2,1]

**Output:** 6

**Explanation:** The above elevation map (black section) is represented by array [0,1,0,2,1,0,1,3,2,1,2,1]. In this case, 6 units of rain water (blue section) are being trapped.

**Example 2:**

**Input:** height = [4,2,0,3,2,5]

**Output:** 9

**Constraints:**

*   `n == height.length`
*   <code>1 <= n <= 2 * 10<sup>4</sup></code>
*   <code>0 <= height[i] <= 10<sup>5</sup></code>

## Solution

```racket
; #Hard #Top_100_Liked_Questions #Top_Interview_Questions #Array #Dynamic_Programming #Two_Pointers
; #Stack #Monotonic_Stack #Dynamic_Programming_I_Day_9 #Udemy_Two_Pointers
; #Top_Interview_150_Array/String #Big_O_Time_O(n)_Space_O(1)
; #2025_02_03_Time_0_(100.00%)_Space_129.13_(100.00%)

(define (trap height)
    (define H (list->vector height))
    
    (define (go water left right L R)
        (cond [(>= left right) water]
              [else 
                (cond [(<= L R) (go (+ water 
                                       (max (- (min L R)
                                               (vector-ref H (add1 left)))
                                            0))
                                    (add1 left) 
                                    right
                                    (max L (vector-ref H (add1 left)))
                                    R)]
                      [else (go (+ water 
                                   (max (- (min L R) 
                                           (vector-ref H (sub1 right)))
                                        0))
                                   left 
                                   (sub1 right)
                                   L
                                   (max R (vector-ref H (sub1 right))))])]))
    (go 0 
        0 
        (sub1 (length height)) 
        (vector-ref H 0) 
        (vector-ref H (sub1 (length height)))))
```