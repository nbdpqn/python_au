# Intervals

+ [Insert Interval](#insert-interval)
+ [Merge Intervals](#merge-intervals)
+ [Non-overlapping Intervals](#non-overlapping-intervals)

## Insert Interval

https://leetcode.com/problems/insert-interval/

```python
def insert(self, intervals: List[List[int]], newInterval: List[int]) -> List[List[int]]:
    sorted_intervals = sorted(intervals + [newInterval], key=lambda x: x[0])
    result = list()
    for interval in sorted_intervals:
        if not result or result[-1][1] < interval[0]:
            result.append(interval)
        else:
            result[-1][1] = max(result[-1][1], interval[1])
    return result
```

## Merge Intervals

https://leetcode.com/problems/merge-intervals/

```python
def merge(self, intervals: List[List[int]]) -> List[List[int]]:
    sorted_intervals = sorted(intervals, key=lambda x: x[0])
    result = list()
    for interval in sorted_intervals:
        if not result or result[-1][1] < interval[0]:
            result.append(interval)
        else:
            result[-1][1] = max(result[-1][1], interval[1])
    return result
```

## Non-overlapping Intervals

https://leetcode.com/problems/non-overlapping-intervals/

```python
def eraseOverlapIntervals(self, intervals: List[List[int]]) -> int:
    if not intervals:
        return 0
    sorted_intervals = sorted(intervals, key=lambda x: x[1])
    right_endpoint = sorted_intervals[0][1]
    counter = 0
    for interval in sorted_intervals[1:]:
        if interval[0] < right_endpoint:
            counter += 1
        else:
            right_endpoint = interval[1]
    return counter
```
