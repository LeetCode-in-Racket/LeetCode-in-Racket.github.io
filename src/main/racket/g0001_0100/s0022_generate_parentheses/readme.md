[![](https://img.shields.io/github/stars/LeetCode-in-Racket/LeetCode-in-Racket?label=Stars&style=flat-square)](https://github.com/LeetCode-in-Racket/LeetCode-in-Racket)
[![](https://img.shields.io/github/forks/LeetCode-in-Racket/LeetCode-in-Racket?label=Fork%20me%20on%20GitHub%20&style=flat-square)](https://github.com/LeetCode-in-Racket/LeetCode-in-Racket/fork)

## 22\. Generate Parentheses

Medium

Given `n` pairs of parentheses, write a function to _generate all combinations of well-formed parentheses_.

**Example 1:**

**Input:** n = 3

**Output:** ["((()))","(()())","(())()","()(())","()()()"]

**Example 2:**

**Input:** n = 1

**Output:** ["()"]

**Constraints:**

*   `1 <= n <= 8`

## Solution

```racket
; #Medium #Top_100_Liked_Questions #Top_Interview_Questions #String #Dynamic_Programming
; #Backtracking #Algorithm_II_Day_11_Recursion_Backtracking #Udemy_Backtracking/Recursion
; #Top_Interview_150_Backtracking #Big_O_Time_O(2^n)_Space_O(n)
; #2025_02_03_Time_3_(100.00%)_Space_101.96_(100.00%)

(define (generate-parenthesis n)
  (let ([res '()])
    (let loop ([opening 0] [closing 0] [path ""])
      (cond ((and (= opening n) (= closing n))
             (set! res (cons path res)))
          (else
            (when (< opening n)
              (loop (add1 opening) closing (string-append path "(")))
            (when (< closing opening)
              (loop opening (add1 closing) (string-append path ")")))))
      res)))
```