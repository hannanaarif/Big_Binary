
# Problem Name: Shortest Subarray With OR at Least K

## 1. Problem Statement
You are given an array `nums` of **non-negative** integers and an integer `k`. An array is called **special** if the bitwise OR of all its elements is **at least** `k`. Return the length of the **shortest special non-empty** *subarray* of `nums`, or return `-1` if no special subarray exists.

## 2. Example Inputs
- **Example 1**:
  - **Input**: nums = [1, 2, 3], k = 2
  - **Output**: 1
  - **Explanation**: The subarray [3] has an OR value of 3, meeting the criteria. Thus, the answer is 1.

- **Example 2**:
  - **Input**: nums = [2, 1, 8], k = 10
  - **Output**: 3
  - **Explanation**: The subarray [2, 1, 8] has an OR value of 11, which is at least `k`. Hence, the length is 3.

- **Example 3**:
  - **Input**: nums = [1, 2], k = 0
  - **Output**: 1
  - **Explanation**: The subarray [1] has an OR value of 1, which is greater than or equal to `k`, so the answer is 1.

## 3. Brute Force Approach

### a. Approach
For each subarray of `nums`, calculate the bitwise OR of its elements and check if it is at least `k`. Track the length of the shortest subarray that meets the condition.

### b. Steps
1. Loop over all starting indices of subarrays.
2. For each start index, calculate the OR of all possible subarrays beginning there.
3. Track the minimum length of subarrays with OR value at least `k`.

### c. Time & Space Complexity
- **Time Complexity**: `O(n^2)` due to evaluating the OR for each subarray.
- **Space Complexity**: `O(1)` since only a few variables are used.

### d. Code Snippet

```javascript
function shortestSubarrayWithORAtLeastKBruteForce(nums, k) {
    let minLength = Infinity;

    for (let i = 0; i < nums.length; i++) {
        let orValue = 0;
        for (let j = i; j < nums.length; j++) {
            orValue |= nums[j];
            if (orValue >= k) {
                minLength = Math.min(minLength, j - i + 1);
                break; // no need to continue if OR is already >= k
            }
        }
    }

    return minLength === Infinity ? -1 : minLength;
}
```

### e. Dry Run
- **Input**: nums = [1, 2, 3], k = 2
- Starting from each element, calculate ORs and find the shortest valid subarray.

## 4. Efficient Approach

### a. Approach (Sliding Window)
Using a sliding window approach, maintain a window with elements that meet the condition (OR >= k). Adjust the window as needed to track the shortest length.

### b. Steps
1. Use a window that expands by moving the `right` pointer and includes each element into the current OR value.
2. If the OR of the current window meets or exceeds `k`, update the shortest length and increment `left` to try for a shorter subarray.
3. Repeat until the end of the array.

### c. Time & Space Complexity
- **Time Complexity**: `O(n)` as each element is considered only once per window.
- **Space Complexity**: `O(1)` as minimal additional storage is used.

### d. Code Snippet

```javascript
function shortestSubarrayWithORAtLeastKEfficient(nums, k) {
    let left = 0;
    let minLength = Infinity;
    let orValue = 0;

    for (let right = 0; right < nums.length; right++) {
        orValue |= nums[right];

        while (orValue >= k) {
            minLength = Math.min(minLength, right - left + 1);
            orValue ^= nums[left];  // Remove nums[left] from OR calculation
            left++;
        }
    }

    return minLength === Infinity ? -1 : minLength;
}
```

### e. Dry Run
- **Input**: nums = [2, 1, 8], k = 10
- Using a sliding window, adjust the window to maintain the shortest length that meets the OR requirement.

## 5. Complexity Analysis

### a. Brute Force Time & Space Complexity
- **Time Complexity**: `O(n^2)`
- **Space Complexity**: `O(1)`

### b. Optimized Time and Space Complexity
- **Time Complexity**: `O(n)`
- **Space Complexity**: `O(1)`

## 6. Conclusion
The brute force approach checks each subarray individually, which is inefficient for larger arrays. The sliding window technique reduces complexity by dynamically maintaining a valid window, providing a faster solution.
