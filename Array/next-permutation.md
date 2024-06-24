# 31. Next Permutation

## Question
A permutation of an array of integers is an arrangement of its members into a sequence or linear order.

For example, for arr = [1,2,3], the following are all the permutations of arr: [1,2,3], [1,3,2], [2, 1, 3], [2, 3, 1], [3,1,2], [3,2,1].
The next permutation of an array of integers is the next lexicographically greater permutation of its integer. More formally, if all the permutations of the array are sorted in one container according to their lexicographical order, then the next permutation of that array is the permutation that follows it in the sorted container. If such arrangement is not possible, the array must be rearranged as the lowest possible order (i.e., sorted in ascending order).

For example, the next permutation of arr = [1,2,3] is [1,3,2].
Similarly, the next permutation of arr = [2,3,1] is [3,1,2].
While the next permutation of arr = [3,2,1] is [1,2,3] because [3,2,1] does not have a lexicographical larger rearrangement.
Given an array of integers nums, find the next permutation of nums.

The replacement must be in place and use only constant extra memory.

## My Solution:
```
class Solution:
    def nextPermutation(self, nums: List[int]) -> None:
        """
        Do not return anything, modify nums in-place instead.
        """

        breakpt = -1
        for i in range(len(nums)-2,-1,-1):
            if nums[i]<nums[i+1]:
                breakpt = i
                break
        print(breakpt)
        if breakpt==-1:
            return nums.reverse()
        else:
            for i in range(len(nums)-1,breakpt,-1):
                if nums[breakpt]<nums[i]:
                    nums[breakpt],nums[i] = nums[i],nums[breakpt]
                    break
        nums[breakpt+1:] = nums[breakpt+1:][::-1]
        print(nums)
```


## Explanation
To solve the problem of finding the next lexicographical permutation of a given array of integers, we need to make use of a specific algorithmic approach that ensures we do this efficiently in-place and with constant extra memory. 

### Steps to Find the Next Permutation
#### Identify the Rightmost Ascent:
Traverse the array from right to left to find the first index i such that nums[i] < nums[i + 1]. This identifies the rightmost point where the sequence ascends.
If no such index exists, it means the array is sorted in descending order, and we need to reverse the entire array to get the smallest permutation (ascending order).

#### Find the Successor to Pivot:
If a valid i is found, traverse the array again from right to left to find the first index j such that nums[j] > nums[i]. This identifies the smallest element larger than the pivot element (nums[i]).

#### Swap Pivot with Successor:
Swap the elements at indices i and j.

#### Reverse the Suffix:
Reverse the sequence from index i + 1 to the end of the array. This step ensures that we get the smallest lexicographical order for the next permutation.

### Explanation of the Algorithm
- Step 1: We find the first pair of consecutive elements from the right where nums[i] < nums[i + 1]. This gives us the rightmost point where the order can be increased.
- Step 2: Once we have the pivot nums[i], we look for the smallest element greater than nums[i] from the rightmost end of the array. This ensures the next permutation is the smallest possible increase.
- Step 3: Swapping these elements ensures we replace nums[i] with the next higher number.
- Step 4: Reversing the sequence after the pivot ensures that the suffix is in the smallest possible order.
### Time and Space Complexity
#### Time Complexity: 
O(n), where n is the length of the array. Each step involves a single pass over the array or a portion of it.
#### Space Complexity: 
O(1), as the operations are done in-place without requiring additional storage.