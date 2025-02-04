[![](https://img.shields.io/github/stars/LeetCode-in-Racket/LeetCode-in-Racket?label=Stars&style=flat-square)](https://github.com/LeetCode-in-Racket/LeetCode-in-Racket)
[![](https://img.shields.io/github/forks/LeetCode-in-Racket/LeetCode-in-Racket?label=Fork%20me%20on%20GitHub%20&style=flat-square)](https://github.com/LeetCode-in-Racket/LeetCode-in-Racket/fork)

## 17\. Letter Combinations of a Phone Number

Medium

Given a string containing digits from `2-9` inclusive, return all possible letter combinations that the number could represent. Return the answer in **any order**.

A mapping of digit to letters (just like on the telephone buttons) is given below. Note that 1 does not map to any letters.

![](https://upload.wikimedia.org/wikipedia/commons/thumb/7/73/Telephone-keypad2.svg/200px-Telephone-keypad2.svg.png)

**Example 1:**

**Input:** digits = "23"

**Output:** ["ad","ae","af","bd","be","bf","cd","ce","cf"]

**Example 2:**

**Input:** digits = ""

**Output:** []

**Example 3:**

**Input:** digits = "2"

**Output:** ["a","b","c"]

**Constraints:**

*   `0 <= digits.length <= 4`
*   `digits[i]` is a digit in the range `['2', '9']`.

## Solution

```racket
; #Medium #Top_100_Liked_Questions #Top_Interview_Questions #String #Hash_Table #Backtracking
; #Algorithm_II_Day_11_Recursion_Backtracking #Udemy_Backtracking/Recursion
; #Top_Interview_150_Backtracking #Big_O_Time_O(4^n)_Space_O(n)
; #2025_02_03_Time_0_(100.00%)_Space_102.48_(_%)

(define (letter-combinations digits)
  (let* ((letters (vector "" "" "abc" "def" "ghi" "jkl" "mno" "pqrs" "tuv" "wxyz"))
         (letters2 (map string->list
                        (map (lambda (x) (vector-ref letters x))
                             (map (lambda (y) (string->number (make-string 1 y)))
                                  (string->list digits))))))
    (if (string=? "" digits)
        '()
        (map list->string (apply cartesian-product letters2)))))
```