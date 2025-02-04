[![](https://img.shields.io/github/stars/LeetCode-in-Racket/LeetCode-in-Racket?label=Stars&style=flat-square)](https://github.com/LeetCode-in-Racket/LeetCode-in-Racket)
[![](https://img.shields.io/github/forks/LeetCode-in-Racket/LeetCode-in-Racket?label=Fork%20me%20on%20GitHub%20&style=flat-square)](https://github.com/LeetCode-in-Racket/LeetCode-in-Racket/fork)

## 2\. Add Two Numbers

Medium

You are given two **non-empty** linked lists representing two non-negative integers. The digits are stored in **reverse order**, and each of their nodes contains a single digit. Add the two numbers and return the sum as a linked list.

You may assume the two numbers do not contain any leading zero, except the number 0 itself.

**Example 1:**

![](https://assets.leetcode.com/uploads/2020/10/02/addtwonumber1.jpg)

**Input:** l1 = [2,4,3], l2 = [5,6,4]

**Output:** [7,0,8]

**Explanation:** 342 + 465 = 807. 

**Example 2:**

**Input:** l1 = [0], l2 = [0]

**Output:** [0] 

**Example 3:**

**Input:** l1 = [9,9,9,9,9,9,9], l2 = [9,9,9,9]

**Output:** [8,9,9,9,0,0,0,1] 

**Constraints:**

*   The number of nodes in each linked list is in the range `[1, 100]`.
*   `0 <= Node.val <= 9`
*   It is guaranteed that the list represents a number that does not have leading zeros.

## Solution

```racket
; #Medium #Top_100_Liked_Questions #Top_Interview_Questions #Math #Linked_List #Recursion
; #Data_Structure_II_Day_10_Linked_List #Programming_Skills_II_Day_15
; #Big_O_Time_O(max(N,M))_Space_O(max(N,M)) #AI_can_be_used_to_solve_the_task
; #2025_01_28_Time_0_(100.00%)_Space_128.42_(12.50%)

; Definition for singly-linked list:
#|

; val : integer?
; next : (or/c list-node? #f)
(struct list-node
  (val next) #:mutable #:transparent)

; constructor
(define (make-list-node [val 0])
  (list-node val #f))

|#

(define/contract (add-two-numbers l1 l2)
  (-> (or/c list-node? #f) (or/c list-node? #f) (or/c list-node? #f))
  (add-two-numbers-help l1 l2 0)
  )

(define (add-two-numbers-help l1 l2 carry-sum)
    (cond
        [(and (false? l1) (false? l2)) (if (zero? carry-sum) #f (list-node carry-sum #f))]
        [(false? l1) (list-node (modulo (+ (list-node-val l2) carry-sum) 10) (add-two-numbers-help l1 (list-node-next l2) (/ (- (+ (list-node-val l2) carry-sum) (modulo (+ (list-node-val l2) carry-sum) 10)) 10)))]
        [(false? l2) (list-node (modulo (+ (list-node-val l1) carry-sum) 10) (add-two-numbers-help (list-node-next l1) l2 (/ (- (+ (list-node-val l1) carry-sum) (modulo (+ (list-node-val l1) carry-sum) 10)) 10)))]
        [else (list-node (modulo (+ (list-node-val l1) (list-node-val l2) carry-sum) 10) (add-two-numbers-help (list-node-next l1) (list-node-next l2) (/ (- (+ (list-node-val l1) (list-node-val l2) carry-sum) (modulo (+ (list-node-val l1) (list-node-val l2) carry-sum) 10)) 10)))]
    )
)
```