[![](https://img.shields.io/github/stars/LeetCode-in-Racket/LeetCode-in-Racket?label=Stars&style=flat-square)](https://github.com/LeetCode-in-Racket/LeetCode-in-Racket)
[![](https://img.shields.io/github/forks/LeetCode-in-Racket/LeetCode-in-Racket?label=Fork%20me%20on%20GitHub%20&style=flat-square)](https://github.com/LeetCode-in-Racket/LeetCode-in-Racket/fork)

## 19\. Remove Nth Node From End of List

Medium

Given the `head` of a linked list, remove the `nth` node from the end of the list and return its head.

**Example 1:**

![](https://assets.leetcode.com/uploads/2020/10/03/remove_ex1.jpg)

**Input:** head = [1,2,3,4,5], n = 2

**Output:** [1,2,3,5]

**Example 2:**

**Input:** head = [1], n = 1

**Output:** []

**Example 3:**

**Input:** head = [1,2], n = 1

**Output:** [1]

**Constraints:**

*   The number of nodes in the list is `sz`.
*   `1 <= sz <= 30`
*   `0 <= Node.val <= 100`
*   `1 <= n <= sz`

**Follow up:** Could you do this in one pass?

## Solution

```racket
; #Medium #Top_100_Liked_Questions #Top_Interview_Questions #Two_Pointers #Linked_List
; #Algorithm_I_Day_5_Two_Pointers #Level_2_Day_3_Linked_List #Top_Interview_150_Linked_List
; #Big_O_Time_O(L)_Space_O(L) #2025_02_03_Time_0_(100.00%)_Space_101.91_(_%)

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

(define (linked-list->numbers ll)
  (if (not (list-node? ll))
      '()
      (append (list (list-node-val ll))
              (linked-list->numbers (list-node-next ll)))))

(define (numbers->linked-list numbers)
  (if (empty? numbers) #f (foldr list-node #f numbers)))

(define (drop-nth-right ls n)
  (append (take ls (- (length ls) n))
          (take-right ls (sub1 n))))

(define (remove-nth-from-end head n)
  (numbers->linked-list (drop-nth-right (linked-list->numbers head) n)))
```