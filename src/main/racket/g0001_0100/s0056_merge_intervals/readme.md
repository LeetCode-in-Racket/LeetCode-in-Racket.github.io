[![](https://img.shields.io/github/stars/LeetCode-in-Racket/LeetCode-in-Racket?label=Stars&style=flat-square)](https://github.com/LeetCode-in-Racket/LeetCode-in-Racket)
[![](https://img.shields.io/github/forks/LeetCode-in-Racket/LeetCode-in-Racket?label=Fork%20me%20on%20GitHub%20&style=flat-square)](https://github.com/LeetCode-in-Racket/LeetCode-in-Racket/fork)

## 56\. Merge Intervals

Medium

Given an array of `intervals` where <code>intervals[i] = [start<sub>i</sub>, end<sub>i</sub>]</code>, merge all overlapping intervals, and return _an array of the non-overlapping intervals that cover all the intervals in the input_.

**Example 1:**

**Input:** intervals = \[\[1,3],[2,6],[8,10],[15,18]]

**Output:** [[1,6],[8,10],[15,18]]

**Explanation:** Since intervals [1,3] and [2,6] overlap, merge them into [1,6].

**Example 2:**

**Input:** intervals = \[\[1,4],[4,5]]

**Output:** [[1,5]]

**Explanation:** Intervals [1,4] and [4,5] are considered overlapping.

**Constraints:**

*   <code>1 <= intervals.length <= 10<sup>4</sup></code>
*   `intervals[i].length == 2`
*   <code>0 <= start<sub>i</sub> <= end<sub>i</sub> <= 10<sup>4</sup></code>

## Solution

```racket
; #Medium #Top_100_Liked_Questions #Top_Interview_Questions #Array #Sorting
; #Data_Structure_II_Day_2_Array #Level_2_Day_17_Interval #Udemy_2D_Arrays/Matrix
; #Top_Interview_150_Intervals #Big_O_Time_O(n_log_n)_Space_O(n)
; #2025_02_03_Time_474_(100.00%)_Space_131.06_(_%)

(define/contract (merge intervals)
  (-> (listof (listof exact-integer?)) (listof (listof exact-integer?)))
  (if (empty? intervals)
      '()
      (let* ([sorted-intervals (sort intervals (λ (a b) (< (first a) (first b))))])
        (let merge-helper ([intervals (rest sorted-intervals)]
                          [result (list (first sorted-intervals))])
          (cond
            [(empty? intervals) result]
            [else
             (let* ([current (last result)]
                    [next (first intervals)]
                    [current-end (second current)]
                    [next-start (first next)]
                    [next-end (second next)])
               (if (<= next-start current-end)
                   ; Merge overlapping intervals
                   (merge-helper 
                    (rest intervals)
                    (append (drop-right result 1)
                           (list (list (first current) 
                                     (max current-end next-end)))))
                   ; Add non-overlapping interval
                   (merge-helper 
                    (rest intervals)
                    (append result (list next)))))])))))
```