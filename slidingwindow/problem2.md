
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

## 4. Efficient Approach

### a. Approach
An efficient approach is to use a frequency map to count occurrences of each number in `nums`. Then, for each unique number, check the length of the harmonious subsequence formed by that number and the number that is exactly one greater.

### b. Steps
1. Create a frequency map of the elements in `nums`.
2. For each unique number, check if the number plus one exists in the map.
3. If it exists, calculate the length of the harmonious subsequence as the sum of the counts of the two numbers.
4. Keep track of the maximum length found.
5. Return the maximum length of the harmonious subsequence.

### c. Time & Space Complexity
- **Time Complexity**: `O(n)` (one pass to count and another to check pairs)
- **Space Complexity**: `O(n)` (for the frequency map)

### d. Code Snippet
```javascript
function findLHS(nums) {
    const frequency = new Map();
    let maxLength = 0;
    
    for (const num of nums) {
        frequency.set(num, (frequency.get(num) || 0) + 1);
    }
    
    for (const [key, count] of frequency) {
        if (frequency.has(key + 1)) {
            maxLength = Math.max(maxLength, count + frequency.get(key + 1));
        }
    }
    
    return maxLength;
}
```

### e. Dry Run
- Input: `nums = [1, 3, 2, 2, 5, 2, 3, 7]`
- Steps:
  1. Create frequency map: `{1: 2, 2: 3, 3: 2, 4: 1, 5: 1}`.
  2. Check for each key: 
     - For `2`: `count = 3`, `key + 1 = 3`: `3 + 2 = 5` (update maxLength).
  3. Final Result: Length = 5.

## 5. Complexity Analysis

### a. Brute Force Time & Space
- **Time Complexity**: `O(2^n * n)`
- **Space Complexity**: `O(n)`

### b. Optimized Time & Space
- **Time Complexity**: `O(n)`
- **Space Complexity**: `O(n)`

## 6. Conclusion
The brute force approach is impractical for larger arrays due to its exponential time complexity. The optimized approach using a frequency map efficiently calculates the length of the longest harmonious subsequence in linear time, making it suitable for larger inputs.
