
# Defuse the Bomb

## 1. Problem Statement
You have a bomb to defuse, and your time is running out! Your informer will provide you with a circular array `code` of length `n` and a key `k`.

To decrypt the code, you must replace every number in the array. All the numbers are replaced simultaneously.

### Replacement Rules
- If `k > 0`, replace the `i-th` number with the sum of the next `k` numbers.
- If `k < 0`, replace the `i-th` number with the sum of the previous `k` numbers.
- If `k == 0`, replace the `i-th` number with `0`.

The array is circular, meaning:
- The next element of `code[n-1]` is `code[0]`.
- The previous element of `code[0]` is `code[n-1]`.

### Goal
Given the circular array `code` and an integer `k`, return the decrypted code to defuse the bomb.

## 2. Example Inputs

- **Example 1:**  
  **Input:** `code = [5,7,1,4]`, `k = 3`  
  **Output:** `[12,10,16,13]`  
  **Explanation:** Each number is replaced by the sum of the next 3 numbers. The decrypted code is `[7+1+4, 1+4+5, 4+5+7, 5+7+1]`.

- **Example 2:**  
  **Input:** `code = [1,2,3,4]`, `k = 0`  
  **Output:** `[0,0,0,0]`  
  **Explanation:** When `k` is zero, all numbers are replaced by `0`.

- **Example 3:**  
  **Input:** `code = [2,4,9,3]`, `k = -2`  
  **Output:** `[12,5,6,13]`  
  **Explanation:** Each number is replaced by the sum of the previous 2 numbers.

## 3. Brute Force Approach

### a. Approach
The brute force approach involves calculating the sum for each position `i` by manually iterating over the next or previous `k` elements. This approach is straightforward but not optimized.

### b. Steps
1. Initialize an empty array `result` to store the decrypted values.
2. For each index `i` in `code`, calculate the sum of the `k` elements that follow or precede it based on `k`'s sign.
3. Append the computed sum to the `result` array.
4. Return `result` as the decrypted code.

### c. Time & Space Complexity
- **Time Complexity:** O(n*k), where `n` is the length of `code` and `k` is the number of elements to sum.
- **Space Complexity:** O(n) for the output array.

### d. Code Snippet
```javascript
function decryptCodeBruteForce(code, k) {
    const n = code.length;
    const result = Array(n).fill(0);

    for (let i = 0; i < n; i++) {
        let sum = 0;
        if (k > 0) {
            for (let j = 1; j <= k; j++) {
                sum += code[(i + j) % n];
            }
        } else if (k < 0) {
            for (let j = 1; j <= -k; j++) {
                sum += code[(i - j + n) % n];
            }
        }
        result[i] = sum;
    }

    return result;
}
```

### e. Dry Run
For `code = [5,7,1,4]` and `k = 3`:
- `i = 0`: `7+1+4 = 12`
- `i = 1`: `1+4+5 = 10`
- `i = 2`: `4+5+7 = 16`
- `i = 3`: `5+7+1 = 13`

**Output:** `[12,10,16,13]`

## 4. Efficient Approach

### a. Approach
Using the sliding window technique, we can reduce unnecessary calculations by keeping a running sum of the last `k` elements.

### b. Steps
1. Initialize an empty array `result` and a variable `windowSum` for the sum of `k` elements.
2. Precompute the first window sum.
3. Slide the window over `code` and update `windowSum` by adding the next element and removing the previous one.
4. Append the updated `windowSum` to `result`.

### c. Time & Space Complexity
- **Time Complexity:** O(n), where `n` is the length of `code`.
- **Space Complexity:** O(n) for the result.

### d. Code Snippet
```javascript
function decryptCodeSlidingWindow(code, k) {
    const n = code.length;
    const result = Array(n).fill(0);

    if (k === 0) return result;

    let windowSum = 0;
    let start = k > 0 ? 1 : n + k;
    let end = k > 0 ? k : n - 1;

    for (let i = start; i <= end; i++) {
        windowSum += code[i % n];
    }

    for (let i = 0; i < n; i++) {
        result[i] = windowSum;
        windowSum -= code[(start++) % n];
        windowSum += code[(++end) % n];
    }

    return result;
}
```

### e. Dry Run
For `code = [5,7,1,4]` and `k = 3`:
- Initial `windowSum`: `7+1+4 = 12`
- Update `result[0] = 12`, then slide window to next elements.

**Output:** `[12,10,16,13]`

## 5. Complexity Analysis
### a. Brute Force
- **Time Complexity:** O(n*k)
- **Space Complexity:** O(n)

### b. Optimized
- **Time Complexity:** O(n)
- **Space Complexity:** O(n)

## 6. Conclusion
This guide demonstrates two approaches for solving the "Defuse the Bomb" problem:
- The brute force approach is simple but has higher time complexity.
- The sliding window approach is more efficient and uses optimized calculations for better performance.
