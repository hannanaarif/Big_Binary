
# Problem Name: Maximum Strong Pair XOR I

## 1. Problem Statement
You are given a 0-indexed integer array `nums`. A pair of integers `x` and `y` is called a strong pair if it satisfies the condition:

|x - y| <= min(x, y)
You need to select two integers from `nums` such that they form a strong pair and their bitwise XOR is the maximum among all strong pairs in the array.

Return the maximum XOR value out of all possible strong pairs in the array `nums`.

Note that you can pick the same integer twice to form a pair.

### Example 1:
- Input: `nums = [1,2,3,4,5]`
- Output: `7`
- Explanation: There are 11 strong pairs in `nums`, with the maximum XOR possible being `3 XOR 4 = 7`.

### Example 2:
- Input: `nums = [10,100]`
- Output: `0`
- Explanation: The maximum XOR is `10 XOR 10 = 0` or `100 XOR 100 = 0`.

### Example 3:
- Input: `nums = [5,6,25,30]`
- Output: `7`
- Explanation: The maximum XOR from strong pairs is `25 XOR 30 = 7`.

## 2. Brute Force Approach

### a. Approach
- Check all possible pairs `(x, y)` in `nums` to identify strong pairs and calculate their XOR.
- Track the maximum XOR among all strong pairs.

### b. Steps
1. Loop through each element in `nums` as `x`.
2. For each `x`, check each element as `y` to form a pair.
3. Check if `|x - y| <= min(x, y)`, making it a strong pair.
4. If it's a strong pair, calculate `x XOR y` and update the maximum XOR.

### c. Time & Space Complexity
- **Time Complexity:** O(n^2), due to the double loop over `nums` for all pairs.
- **Space Complexity:** O(1).

### d. Code Snippet
```javascript
function maximumStrongPairXOR(nums) {
  let maxXor = 0;

  for (let i = 0; i < nums.length; i++) {
    for (let j = i; j < nums.length; j++) {
      const x = nums[i], y = nums[j];
      if (Math.abs(x - y) <= Math.min(x, y)) {
        maxXor = Math.max(maxXor, x ^ y);
      }
    }
  }

  return maxXor;
}
```

### e. Dry Run
- For `nums = [1,2,3,4,5]`, the algorithm calculates the XOR values for valid pairs and finds the maximum XOR `3 XOR 4 = 7`.

## 3. Efficient Approach (Sliding Window)

### a. Approach
- Use the sliding window approach with sorting to reduce the number of checks.
- Slide over `nums` and maintain a window of strong pairs with minimal checks.

### b. Steps
1. Sort `nums` to simplify the strong pair condition check.
2. Slide through `nums`, forming pairs `nums[i]` and `nums[j]` within the window.
3. Check the strong pair condition and calculate XOR.
4. Track the maximum XOR.

### c. Time & Space Complexity
- **Time Complexity:** O(n log n) due to sorting and O(n) for single pass.
- **Space Complexity:** O(1).

### d. Code Snippet
```javascript
function maximumStrongPairXOR(nums) {
  nums.sort((a, b) => a - b);
  let maxXor = 0;

  for (let i = 0; i < nums.length; i++) {
    for (let j = i; j < nums.length && Math.abs(nums[i] - nums[j]) <= Math.min(nums[i], nums[j]); j++) {
      maxXor = Math.max(maxXor, nums[i] ^ nums[j]);
    }
  }

  return maxXor;
}
```

### e. Dry Run
- For `nums = [5,6,25,30]`, the sorted list is checked, and the valid strong pair `(25, 30)` gives the max XOR `7`.

## 4. Complexity Analysis

### a. Brute Force
- **Time Complexity:** O(n^2)
- **Space Complexity:** O(1)

### b. Optimized
- **Time Complexity:** O(n log n) (due to sorting and single traversal)
- **Space Complexity:** O(1)

## 5. Conclusion
- The brute force method is straightforward but inefficient.
- The optimized approach uses sorting to reduce the complexity, making it better suited for larger arrays.
