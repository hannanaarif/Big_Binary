
# Problem Name: Minimum Difference Between Highest and Lowest of K Scores

## 1. Problem Statement
You are given a 0-indexed integer array `nums`, where `nums[i]` represents the score of the ith student. You are also given an integer `k`.

Pick the scores of any `k` students from the array so that the difference between the highest and the lowest of the `k` scores is minimized.

Return the minimum possible difference.

### Constraints:
- `1 <= k <= nums.length <= 1000`
- `0 <= nums[i] <= 10^5`

## 2. Example Inputs and Outputs

- **Example 1:**
    - Input: `nums = [90], k = 1`
    - Output: `0`
    - Explanation: There is one way to pick score(s) of one student: `[90]`. The difference between the highest and lowest score is `90 - 90 = 0`. The minimum possible difference is `0`.

- **Example 2:**
    - Input: `nums = [9,4,1,7], k = 2`
    - Output: `2`
    - Explanation: There are several ways to pick scores of two students, including:
      - `[9, 7]` (difference is `2`)
      - `[4, 1]` (difference is `3`)
      The minimum possible difference is `2`.

## 3. Brute Force Approach

### a. Approach
The brute-force approach involves examining all possible sets of `k` scores and calculating the difference between the highest and lowest scores in each set, selecting the minimum difference found.

### b. Steps
1. Generate all possible combinations of `k` scores from `nums`.
2. For each combination, find the maximum and minimum scores.
3. Calculate the difference between the maximum and minimum scores.
4. Track the smallest difference.

### c. Time & Space Complexity
- **Time Complexity:** O(n^k), due to generating all subsets of size `k`.
- **Space Complexity:** O(k), for storing each subset temporarily.

### d. Code Snippet

```javascript
function minimumDifference(nums, k) {
    if (k === 1) return 0;

    let minDiff = Infinity;

    for (let i = 0; i <= nums.length - k; i++) {
        for (let j = i; j < i + k; j++) {
            const subset = nums.slice(i, i + k);
            const diff = Math.max(...subset) - Math.min(...subset);
            minDiff = Math.min(minDiff, diff);
        }
    }
    return minDiff;
}
```

### e. Dry Run
- Input: `nums = [9,4,1,7], k = 2`
- Output: `2` by calculating the minimum difference in all subsets of size `k=2`.

## 4. Efficient Approach (Sliding Window)

### a. Approach
The efficient approach leverages sorting and the sliding window technique. By sorting `nums`, the minimum difference between the largest and smallest elements in a `k`-length window will yield the desired minimum.

### b. Steps
1. Sort the array `nums`.
2. For each consecutive `k`-length subset of `nums`, calculate the difference between the last and first elements in the window.
3. Track and return the minimum difference.

### c. Time & Space Complexity
- **Time Complexity:** O(n log n) for sorting, and O(n) for finding the minimum difference in a sliding window.
- **Space Complexity:** O(1), if sorting is done in-place.

### d. Code Snippet

```javascript
function minimumDifference(nums, k) {
    if (k === 1) return 0;

    nums.sort((a, b) => a - b);
    let minDiff = Infinity;

    for (let i = 0; i <= nums.length - k; i++) {
        const diff = nums[i + k - 1] - nums[i];
        minDiff = Math.min(minDiff, diff);
    }

    return minDiff;
}
```

### e. Dry Run
- Input: `nums = [9,4,1,7], k = 2`
- After sorting, sliding through the array yields a minimum difference of `2`.

## 5. Complexity Analysis

### a. Brute Force Time & Space Complexity
- **Time Complexity:** O(n^k)
- **Space Complexity:** O(k)

### b. Optimized Time & Space Complexity
- **Time Complexity:** O(n log n)
- **Space Complexity:** O(1)

## 6. Conclusion
The brute-force approach quickly becomes inefficient as `n` and `k` grow due to the exponential time complexity. The sliding window approach, however, provides a much faster solution by leveraging sorting to focus only on contiguous subsets, significantly reducing computation time.
