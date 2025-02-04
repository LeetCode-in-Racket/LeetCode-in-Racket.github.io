[![](https://img.shields.io/github/stars/LeetCode-in-Racket/LeetCode-in-Racket?label=Stars&style=flat-square)](https://github.com/LeetCode-in-Racket/LeetCode-in-Racket)
[![](https://img.shields.io/github/forks/LeetCode-in-Racket/LeetCode-in-Racket?label=Fork%20me%20on%20GitHub%20&style=flat-square)](https://github.com/LeetCode-in-Racket/LeetCode-in-Racket/fork)

## 5\. Longest Palindromic Substring

Medium

Given a string `s`, return _the longest palindromic substring_ in `s`.

**Example 1:**

**Input:** s = "babad"

**Output:** "bab" **Note:** "aba" is also a valid answer. 

**Example 2:**

**Input:** s = "cbbd"

**Output:** "bb" 

**Example 3:**

**Input:** s = "a"

**Output:** "a" 

**Example 4:**

**Input:** s = "ac"

**Output:** "a" 

**Constraints:**

*   `1 <= s.length <= 1000`
*   `s` consist of only digits and English letters.

## Solution

```racket
; #Medium #Top_100_Liked_Questions #Top_Interview_Questions #String #Dynamic_Programming
; #Data_Structure_II_Day_9_String #Algorithm_II_Day_14_Dynamic_Programming
; #Dynamic_Programming_I_Day_17 #Udemy_Strings #Big_O_Time_O(n)_Space_O(n)
; #2025_01_28_Time_10_(50.00%)_Space_102.35_(50.00%)

(define (longest-palindrome s)
  (define (expand-around-center s left right)
    (let loop ([l left] [r right])
      (if (and (>= l 0)
               (< r (string-length s))
               (char=? (string-ref s l) (string-ref s r)))
          (loop (sub1 l) (add1 r))
          (values (add1 l) (sub1 r))))) ;; Return correct boundaries

  (define (find-longest-palindrome s)
    (define len (string-length s))
    (define start 0)
    (define end 0)
    (for ([i (in-range len)])
      ;; Odd-length palindromes centered at i
      (define-values (l1 r1) (expand-around-center s i i))
      ;; Even-length palindromes centered between i and i + 1
      (define-values (l2 r2) (expand-around-center s i (add1 i)))
      
      ;; Update the maximum length palindrome if necessary
      (when (> (- r1 l1) (- end start))
        (set! start l1)
        (set! end r1))
      (when (> (- r2 l2) (- end start))
        (set! start l2)
        (set! end r2)))
    (substring s start (add1 end))) 

  (find-longest-palindrome s))
```