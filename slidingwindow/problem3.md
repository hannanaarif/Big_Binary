
# Problem Name: Maximum Average Subarray I

## 1. Problem Statement
You are given an integer array `nums` consisting of `n` elements, and an integer `k`. Find a contiguous subarray whose length is equal to `k` that has the maximum average value and return this value. Any answer with a calculation error less than `10^-5` will be accepted.

## 2. Example Inputs

- **Example 1:**
    - Input: `nums = [1,12,-5,-6,50,3], k = 4`
    - Output: `12.75000`
    - Explanation: Maximum average is `(12 - 5 - 6 + 50) / 4 = 51 / 4 = 12.75`.

- **Example 2:**
    - Input: `nums = [5], k = 1`
    - Output: `5.00000`

### Constraints
- `n == nums.length`
- `1 <= k <= n <= 10^5`
- `-10^4 <= nums[i] <= 10^4`

## 3. Brute Force Approach

### a. Approach
The brute force approach involves calculating the average of every possible subarray of length `k`, keeping track of the maximum found average.

### b. Steps
1. Initialize `max_avg` as the lowest possible value.
2. Iterate over each starting point `i` of a subarray of length `k` in `nums`.
3. Calculate the sum of elements from `i` to `i+k-1` and determine the average.
4. Update `max_avg` if this average is greater than the previous `max_avg`.
5. Return `max_avg`.

### c. Time & Space Complexity
- **Time Complexity**: `O(n * k)`
- **Space Complexity**: `O(1)`

### d. Code Snippet
```javascript
function findMaxAverage(nums, k) {
    let maxAvg = -Infinity;

    for (let i = 0; i <= nums.length - k; i++) {
        let sum = 0;
        for (let j = 0; j < k; j++) {
            sum += nums[i + j];
        }
        let avg = sum / k;
        maxAvg = Math.max(maxAvg, avg);
    }

    return maxAvg;
}
```

### e. Dry Run
- Input: `nums = [1,12,-5,-6,50,3], k = 4`
- Steps:
  - i=0: Sum=2, Avg=0.5
  - i=1: Sum=51, Avg=12.75 → `maxAvg` updated.

## 4. Efficient Approach (Sliding Window)

### a. Approach
Using a sliding window, we maintain the sum of the current window of length `k`. As we slide the window one element to the right, we subtract the element that goes out of the window and add the element that comes into the window.

### b. Steps
1. Calculate the sum of the first `k` elements as the initial window sum.
2. Initialize `maxSum` as this sum.
3. Slide the window through the array:
   - For each new position, update the sum by subtracting the element that is sliding out and adding the element coming in.
   - Update `maxSum` if the new window sum is greater.
4. Return `maxSum / k` as the maximum average.

### c. Time & Space Complexity
- **Time Complexity**: `O(n)` (only one pass is needed)
- **Space Complexity**: `O(1)`

### d. Code Snippet
```javascript
function findMaxAverage(nums, k) {
    let windowSum = 0;
    
    // Calculate initial window sum
    for (let i = 0; i < k; i++) {
        windowSum += nums[i];
    }

    let maxSum = windowSum;

    // Slide the window
    for (let i = k; i < nums.length; i++) {
        windowSum = windowSum - nums[i - k] + nums[i];
        maxSum = Math.max(maxSum, windowSum);
    }

    return maxSum / k;
}
```

### e. Dry Run
- Input: `nums = [1,12,-5,-6,50,3], k = 4`
- Steps:
  1. Initial Sum = 2, MaxSum = 2
  2. Slide right, update to 51 → MaxSum = 51.
  3. Continue updating → Max average = 12.75.

## 5. Complexity Analysis

### a. Brute Force Time & Space
- **Time Complexity**: `O(n * k)`
- **Space Complexity**: `O(1)`

### b. Optimized Time & Space
- **Time Complexity**: `O(n)`
- **Space Complexity**: `O(1)`

## 6. Conclusion
The brute force approach becomes infeasible for large inputs due to its `O(n * k)` time complexity. The sliding window approach efficiently computes the maximum average in `O(n)` time by reusing the previous window sum, making it optimal for large arrays.
