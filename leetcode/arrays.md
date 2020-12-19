# Arrays

+ [Subarray Sum Equals K](#subarray-sum-equals-k)
+ [3Sum](#3sum)
+ [Two Sum](#two-sum)

## Subarray Sum Equals K

https://leetcode.com/problems/subarray-sum-equals-k/

```python
def subarraySum(self, nums: List[int], k: int) -> int:
    counter = 0
    total_sum = 0
    d = {0: 1}
    for num in nums:
        total_sum += num
        if total_sum - k in d.keys():
            counter += d.get(total_sum - k)
        d.update({total_sum: d.setdefault(total_sum, 0) + 1})
    return counter
```

## 3Sum

https://leetcode.com/problems/3sum/

```python
def threeSum(self, nums: List[int]) -> List[List[int]]:
    sorted_nums = sorted(nums)
    result = list()
    for first in range(len(sorted_nums) - 2):
        if first > 0 and sorted_nums[first] == sorted_nums[first - 1]:
            continue
        second = first + 1
        third = len(sorted_nums) - 1
        while second < third:
            total_sum = sorted_nums[first] + sorted_nums[second] + sorted_nums[third]
            if total_sum < 0:
                second += 1
            elif total_sum > 0:
                third -= 1
            else:
                result.append([sorted_nums[first], sorted_nums[second], sorted_nums[third]])
                while second < third and sorted_nums[second] == sorted_nums[second + 1]:
                    second += 1
                while third > second and sorted_nums[third] == sorted_nums[third - 1]:
                    third -= 1
                second += 1
                third -= 1
    return result
```

## Two Sum

https://leetcode.com/problems/two-sum/

```python
def twoSum(self, nums: List[int], target: int) -> List[int]:
    sorted_nums = sorted(enumerate(nums), key=lambda x: x[1])

    first = 0
    second = len(sorted_nums) - 1
    while first != second:
        if sorted_nums[first][1] + sorted_nums[second][1] == target:
            return [sorted_nums[first][0], sorted_nums[second][0]]
        elif sorted_nums[first][1] + sorted_nums[second][1] < target:
            first += 1
        else:
            second -= 1
```
