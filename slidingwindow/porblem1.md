
# Problem Name: Contains Duplicate II

## 1. Problem Statement
Given an integer array `nums` and an integer `k`, return `true` if there are two distinct indices `i` and `j` in the array such that `nums[i] == nums[j]` and `abs(i - j) <= k`.

### Constraints
- `1 <= nums.length <= 10^5`
- `-10^9 <= nums[i] <= 10^9`
- `0 <= k <= 10^5`

## 2. Example Inputs

- **Example 1:**
    - Input: `nums = [1, 2, 3, 1]`, `k = 3`
    - Output: `true`

- **Example 2:**
    - Input: `nums = [1, 0, 1, 1]`, `k = 1`
    - Output: `true`

## 3. Brute Force Approach

### a. Approach
The brute force approach involves checking all possible pairs of elements in `nums` to determine if there exists a pair of indices `(i, j)` such that `nums[i] == nums[j]` and `|i - j| <= k`. This approach iterates over each element and checks every subsequent element within range `k`.

### b. Steps
1. Start from the first element in `nums`.
2. For each element, check each subsequent element up to `k` indices ahead.
3. If `nums[i] == nums[j]` and `|i - j| <= k`, return `true`.
4. If no such pair is found after checking all elements, return `false`.

### c. Time & Space Complexity
- **Time Complexity**: `O(n * k)`
- **Space Complexity**: `O(1)` (no additional space used)

### d. Code Snippet
```javascript
function containsNearbyDuplicate(nums, k) {
    for (let i = 0; i < nums.length; i++) {
        for (let j = i + 1; j <= i + k && j < nums.length; j++) {
            if (nums[i] === nums[j]) {
                return true;
            }
        }
    }
    return false;
}
```

### e. Dry Run
- Input: `nums = [1, 2, 3, 1]`, `k = 3`
- Steps:
  1. `i = 0`: `nums[0] = 1`
     - `j = 1`: `nums[1] = 2` (not equal)
     - `j = 2`: `nums[2] = 3` (not equal)
     - `j = 3`: `nums[3] = 1` (equal and `|3 - 0| = 3 <= k`)
  2. **Result: true**

## 4. Efficient Approach

### a. Approach
An efficient way to solve this problem is by using a HashMap to store the index of each element. As we iterate through `nums`, we check if the current element exists in the HashMap and if the difference in indices is within the range `k`.

### b. Steps
1. Initialize an empty HashMap.
2. For each element `nums[i]`, check if it exists in the HashMap and if `|i - index| <= k`.
3. If so, return `true`.
4. If not, update the element's index in the HashMap and continue.
5. If no such pair is found, return `false`.

### c. Time & Space Complexity
- **Time Complexity**: `O(n)`
- **Space Complexity**: `O(min(n, k))`

### d. Code Snippet
```javascript
function containsNearbyDuplicate(nums, k) {
    const map = new Map();
    for (let i = 0; i < nums.length; i++) {
        if (map.has(nums[i]) && i - map.get(nums[i]) <= k) {
            return true;
        }
        map.set(nums[i], i);
    }
    return false;
}
```

### e. Dry Run
- Input: `nums = [1, 2, 3, 1]`, `k = 3`
- Steps:
  1. `i = 0`: `nums[0] = 1`, store `map = {1: 0}`
  2. `i = 1`: `nums[1] = 2`, store `map = {1: 0, 2: 1}`
  3. `i = 2`: `nums[2] = 3`, store `map = {1: 0, 2: 1, 3: 2}`
  4. `i = 3`: `nums[3] = 1` exists in `map`, `|3 - 0| = 3 <= k`
  5. **Result: true**

### a. Brute Force Time & Space
- **Time Complexity**: `O(n * k)`
- **Space Complexity**: `O(1)`

### b. Optimized Time & Space
- **Time Complexity**: `O(n)`
- **Space Complexity**: `O(min(n, k))`

## 5. Conclusion
The brute force approach is straightforward but inefficient for large inputs due to its `O(n * k)` complexity. The optimized approach using a HashMap allows for an efficient `O(n)` solution by storing previously encountered indices, making it suitable for large arrays.
