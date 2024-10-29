
# Problem Name: Longest Harmonious Subsequence

## 1. Problem Statement
We define a harmonious array as an array where the difference between its maximum value and its minimum value is exactly 1. Given an integer array `nums`, return the length of its longest harmonious subsequence among all its possible subsequences.

## 2. Example Inputs

- **Example 1:**
    - Input: `nums = [1, 3, 2, 2, 5, 2, 3, 7]`
    - Output: `5`  
      Explanation: The longest harmonious subsequence is `[3, 2, 2, 2, 3]`.

- **Example 2:**
    - Input: `nums = [1, 2, 3, 4]`
    - Output: `2`  
      Explanation: The longest harmonious subsequences are `[1, 2]`, `[2, 3]`, and `[3, 4]`, all of which have a length of `2`.

- **Example 3:**
    - Input: `nums = [1, 1, 1, 1]`
    - Output: `0`  
      Explanation: No harmonic subsequence exists.

### Constraints
- `1 <= nums.length <= 2 * 10^4`
- `-10^9 <= nums[i] <= 10^9`

## 3. Brute Force Approach

### a. Approach
The brute force approach involves generating all possible subsequences of the array `nums` and checking each subsequence to see if it is harmonious (i.e., the maximum and minimum values differ by exactly 1). This can be inefficient due to the potentially large number of subsequences.

### b. Steps
1. Generate all possible subsequences of `nums`.
2. For each subsequence, find the maximum and minimum values.
3. Check if the difference between the maximum and minimum values is 1.
4. Keep track of the length of the longest harmonious subsequence found.
5. Return the length of the longest harmonious subsequence.

### c. Time & Space Complexity
- **Time Complexity**: `O(2^n * n)` (due to generating subsequences and checking each one)
- **Space Complexity**: `O(n)` (for storing the subsequences)

### d. Code Snippet
```javascript
function findLHS(nums) {
    const subsequences = generateSubsequences(nums);
    let maxLength = 0;
    
    for (const subseq of subsequences) {
        const maxVal = Math.max(...subseq);
        const minVal = Math.min(...subseq);
        
        if (maxVal - minVal === 1) {
            maxLength = Math.max(maxLength, subseq.length);
        }
    }
    
    return maxLength;
}

function generateSubsequences(nums) {
    const subsequences = [];
    const n = nums.length;
    
    for (let i = 0; i < (1 << n); i++) {
        const subseq = [];
        for (let j = 0; j < n; j++) {
            if (i & (1 << j)) {
                subseq.push(nums[j]);
            }
        }
        subsequences.push(subseq);
    }
    
    return subsequences;
}
```

### e. Dry Run
- Input: `nums = [1, 3, 2, 2, 5, 2, 3, 7]`
- Steps:
  1. Generate all subsequences (e.g., `[], [1], [3], ...`).
  2. Check subsequences such as `[3, 2, 2, 2, 3]`:
     - Max = 3, Min = 2, Difference = 1, Length = 5 (update maxLength).
  3. Final Result: Length = 5.

## 4. Efficient Approach (Sliding Window)

### a. Approach
Using a sliding window, we can look for harmonious subsequences by moving a window across the sorted array. This ensures that any harmonious subsequence found has adjacent elements differing by at most 1.

### b. Steps
1. Sort the array `nums`.
2. Use two pointers (`start` and `end`) to create a window.
3. Expand the window by moving the `end` pointer until the difference between `nums[end]` and `nums[start]` is greater than 1.
4. When the difference becomes greater than 1, move the `start` pointer to maintain a harmonious window.
5. Track the maximum length of harmonious subsequences found in each window.

### c. Time & Space Complexity
- **Time Complexity**: `O(n log n)` (sorting)
- **Space Complexity**: `O(1)`

### d. Code Snippet
```javascript
function findLHS(nums) {
    nums.sort((a, b) => a - b);
    let start = 0;
    let maxLength = 0;

    for (let end = 1; end < nums.length; end++) {
        while (nums[end] - nums[start] > 1) {
            start++;
        }
        if (nums[end] - nums[start] === 1) {
            maxLength = Math.max(maxLength, end - start + 1);
        }
    }

    return maxLength;
}
```

### e. Dry Run
- Input: `nums = [1, 3, 2, 2, 5, 2, 3, 7]`
- Steps:
  1. Sort `nums` to get `[1, 2, 2, 2, 3, 3, 5, 7]`.
  2. Slide window: check subsequences `[2, 2, 2, 3]` and `[3, 2, 2, 2, 3]`.
  3. Final Result: Length = 5.

## 5. Complexity Analysis

### a. Brute Force Time & Space
- **Time Complexity**: `O(2^n * n)`
- **Space Complexity**: `O(n)`

### b. Optimized Time & Space
- **Time Complexity**: `O(n log n)`
- **Space Complexity**: `O(1)`

## 6. Conclusion
The brute force approach is impractical for larger arrays due to its exponential time complexity. The optimized approach using a sliding window over a sorted array provides an efficient solution with a time complexity of `O(n log n)`, making it suitable for larger inputs.
