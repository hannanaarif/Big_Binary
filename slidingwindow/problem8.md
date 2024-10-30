
# Problem Name: Find the K-Beauty of a Number

## 1. Problem Statement
The k-beauty of an integer `num` is defined as the number of substrings of `num` when it is read as a string that meet the following conditions:
- It has a length of `k`.
- It is a divisor of `num`.

Given integers `num` and `k`, return the k-beauty of `num`.

### Notes:
- Leading zeros are allowed.
- 0 is not a divisor of any value.
- A substring is a contiguous sequence of characters in a string.

### Constraints:
- `1 <= num <= 10^9`
- `1 <= k <= num.length` (taking `num` as a string).

## 2. Example Inputs and Outputs

- **Example 1:**
    - Input: `num = 240, k = 2`
    - Output: `2`
    - Explanation: The substrings of length `k` are:
        - `"24"` from `"240"`: 24 is a divisor of 240.
        - `"40"` from `"240"`: 40 is a divisor of 240.
      Therefore, the k-beauty is `2`.

- **Example 2:**
    - Input: `num = 430043, k = 2`
    - Output: `2`
    - Explanation: The substrings of length `k` include:
        - `"43"`: 43 is a divisor of 430043.
        - `"30"`: 30 is not a divisor of 430043.
        - `"00"`: 0 is not a divisor.
        - `"04"`: 4 is not a divisor of 430043.
        - `"43"`: 43 is a divisor of 430043.
      Thus, the k-beauty is `2`.

## 3. Brute Force Approach

### a. Approach
The brute-force approach involves generating all possible substrings of length `k` and checking if each substring is a divisor of `num`.

### b. Steps
1. Convert `num` to a string.
2. Loop through each starting index up to `num.length - k`.
3. For each substring of length `k`, check if it is non-zero and a divisor of `num`.
4. Count each valid divisor.

### c. Time & Space Complexity
- **Time Complexity:** O(n * k), where `n` is the length of `num` as a string.
- **Space Complexity:** O(1), for counting valid divisors.

### d. Code Snippet

```javascript
function kBeauty(num, k) {
    let numStr = num.toString();
    let count = 0;

    for (let i = 0; i <= numStr.length - k; i++) {
        const substring = parseInt(numStr.slice(i, i + k));
        if (substring !== 0 && num % substring === 0) {
            count++;
        }
    }
    return count;
}
```

### e. Dry Run
- Input: `num = 240, k = 2`
- Output: `2` after evaluating each substring of length `k`.

## 4. Efficient Approach (Sliding Window)

### a. Approach
The sliding window approach keeps a window of length `k` on `num` in string form, moving it one character at a time. Each time, we convert the window substring to an integer and check if it is a divisor.

### b. Steps
1. Convert `num` to a string.
2. Initialize a sliding window of size `k`.
3. For each window position, convert the substring to an integer and check if it is a divisor of `num`.
4. Count valid divisors and slide the window to the right until the end of the string.

### c. Time & Space Complexity
- **Time Complexity:** O(n), where `n` is the length of `num` as a string.
- **Space Complexity:** O(1).

### d. Code Snippet

```javascript
function kBeauty(num, k) {
    let numStr = num.toString();
    let count = 0;

    for (let i = 0; i <= numStr.length - k; i++) {
        const substring = parseInt(numStr.slice(i, i + k));
        if (substring !== 0 && num % substring === 0) {
            count++;
        }
    }
    return count;
}
```

### e. Dry Run
- Input: `num = 430043, k = 2`
- After iterating through each substring, valid divisors include `43` twice, resulting in a k-beauty of `2`.

## 5. Complexity Analysis

### a. Brute Force Time & Space Complexity
- **Time Complexity:** O(n * k)
- **Space Complexity:** O(1)

### b. Optimized Time & Space Complexity
- **Time Complexity:** O(n)
- **Space Complexity:** O(1)

## 6. Conclusion
The brute-force and sliding window approaches are similar in time complexity. However, the sliding window approach is more intuitive and highlights the advantage of fixed-window techniques in substring-based problems, making it a good choice for beginner-friendly optimization.