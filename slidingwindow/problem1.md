
# Problem Name: Contains Duplicate II

## 1. Problem Statement
Given an integer array `nums` and an integer `k`, return `true` if there are two distinct indices `i` and `j` in the array such that `nums[i] == nums[j]` and `abs(i - j) <= k`.

## 2. Example Inputs

- **Example 1:**
    - Input: `nums = [1,2,3,1], k = 3`
    - Output: `true`

- **Example 2:**
    - Input: `nums = [1,0,1,1], k = 1`
    - Output: `true`

### Constraints
- `1 <= nums.length <= 10^5`
- `-10^9 <= nums[i] <= 10^9`
- `0 <= k <= 10^5`

## 3. Brute Force Approach

### a. Approach
The brute force approach involves comparing each element with every other element within the given distance `k`. We iterate over each index and for each index, check all other indices up to `k` steps away.

### b. Steps
1. Iterate through the array with a nested loop.
2. For each element at index `i`, check the elements at indices from `i+1` to `i+k`.
3. If any of these elements is equal to `nums[i]`, return `true`.
4. If no such elements are found, return `false`.

### c. Time & Space Complexity
- **Time Complexity**: `O(n * k)`
- **Space Complexity**: `O(1)`

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
- Input: `nums = [1, 2, 3, 1], k = 3`
- Steps:
  - i=0, j=1,2,3: finds `nums[0] == nums[3]` → returns `true`.

## 4. Efficient Approach (Sliding Window)

### a. Approach
Using a sliding window with a set, we can maintain only the last `k` elements in a window to check for duplicates efficiently. As we slide the window, we add the new element and remove the element that is now out of range.

### b. Steps
1. Initialize an empty set to store elements within the current window.
2. Traverse the array:
   - Check if the current element already exists in the set. If it does, return `true`.
   - Add the current element to the set.
   - If the set size exceeds `k`, remove the element at `i-k` to maintain the window size.
3. If no duplicates are found within range `k`, return `false`.

### c. Time & Space Complexity
- **Time Complexity**: `O(n)` (due to set operations which are `O(1)` on average)
- **Space Complexity**: `O(k)` (to maintain the set of `k` elements)

### d. Code Snippet
```javascript
function containsNearbyDuplicate(nums, k) {
    const windowSet = new Set();

    for (let i = 0; i < nums.length; i++) {
        if (windowSet.has(nums[i])) {
            return true;
        }
        windowSet.add(nums[i]);
        if (windowSet.size > k) {
            windowSet.delete(nums[i - k]);
        }
    }

    return false;
}
```

### e. Dry Run
- Input: `nums = [1,2,3,1], k = 3`
- Steps:
  1. i=0: Add `1` to set.
  2. i=1: Add `2` to set.
  3. i=2: Add `3` to set.
  4. i=3: `1` is already in the set → returns `true`.

## 5. Complexity Analysis

### a. Brute Force Time & Space
- **Time Complexity**: `O(n * k)`
- **Space Complexity**: `O(1)`

### b. Optimized Time & Space
- **Time Complexity**: `O(n)`
- **Space Complexity**: `O(k)`

## 6. Conclusion
The brute force approach is feasible for small inputs but becomes inefficient for large inputs due to its `O(n * k)` time complexity. The optimized approach using a sliding window and set allows us to check for nearby duplicates within `O(n)` time, making it much more efficient for large arrays.
