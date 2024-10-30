
# Problem Name: Minimum Recolors to Get K Consecutive Black Blocks

## 1. Problem Statement
You are given a 0-indexed string `blocks` of length `n`, where `blocks[i]` is either 'W' or 'B', representing the color of the i-th block. The characters 'W' and 'B' denote the colors white and black, respectively.

You are also given an integer `k`, which is the desired number of consecutive black blocks.

In one operation, you can recolor a white block such that it becomes a black block.

Return the minimum number of operations needed such that there is at least one occurrence of `k` consecutive black blocks.

### Constraints:
- `n == blocks.length`
- `1 <= n <= 100`
- `blocks[i]` is either 'W' or 'B'.
- `1 <= k <= n`.

## 2. Example Inputs and Outputs

- **Example 1:**
    - Input: `blocks = "WBBWWBBWBW", k = 7`
    - Output: `3`
    - Explanation: Recoloring the 0th, 3rd, and 4th blocks results in `"BBBBBBBWBW"`, which has 7 consecutive black blocks.

- **Example 2:**
    - Input: `blocks = "WBWBBBW", k = 2`
    - Output: `0`
    - Explanation: The input already has 2 consecutive black blocks, so no recoloring is needed.

## 3. Brute Force Approach

### a. Approach
The brute-force approach involves checking every possible substring of length `k` in `blocks`, counting the white blocks in each substring, and tracking the minimum number of white blocks across all possible substrings.

### b. Steps
1. Loop through each possible substring of length `k`.
2. Count the white blocks in each substring.
3. Track the minimum number of white blocks across all substrings.
4. Return the minimum count as it represents the fewest recolors needed.

### c. Time & Space Complexity
- **Time Complexity:** O(n * k), where `n` is the length of `blocks`.
- **Space Complexity:** O(1), for tracking minimum operations.

### d. Code Snippet

```javascript
function minimumRecolors(blocks, k) {
    let minOperations = Infinity;
    
    for (let i = 0; i <= blocks.length - k; i++) {
        let currentWhiteCount = 0;
        
        for (let j = i; j < i + k; j++) {
            if (blocks[j] === 'W') currentWhiteCount++;
        }
        
        minOperations = Math.min(minOperations, currentWhiteCount);
    }
    
    return minOperations;
}
```

### e. Dry Run
- Input: `blocks = "WBBWWBBWBW", k = 7`
- Check all possible substrings, and find the minimum white blocks needing recoloring, resulting in `3`.

## 4. Efficient Approach (Sliding Window)

### a. Approach
The sliding window approach maintains a window of length `k` and slides it across `blocks`. For each new position, we adjust the count of white blocks by checking only the entering and exiting blocks, avoiding redundant counting.

### b. Steps
1. Initialize a window of length `k` and count the white blocks within it.
2. Slide the window by one position each time, adjusting the white count by adding the new block's color and removing the exiting block's color.
3. Track the minimum number of white blocks required to recolor as the window moves.
4. Return this minimum count.

### c. Time & Space Complexity
- **Time Complexity:** O(n), where `n` is the length of `blocks`.
- **Space Complexity:** O(1).

### d. Code Snippet

```javascript
function minimumRecolors(blocks, k) {
    let whiteCount = 0;
    for (let i = 0; i < k; i++) {
        if (blocks[i] === 'W') whiteCount++;
    }

    let minOperations = whiteCount;

    for (let i = k; i < blocks.length; i++) {
        if (blocks[i] === 'W') whiteCount++;
        if (blocks[i - k] === 'W') whiteCount--;
        
        minOperations = Math.min(minOperations, whiteCount);
    }

    return minOperations;
}
```

### e. Dry Run
- Input: `blocks = "WBWBBBW", k = 2`
- After sliding the window and adjusting white counts, the minimum recolors needed is found to be `0`.

## 5. Complexity Analysis

### a. Brute Force Time & Space Complexity
- **Time Complexity:** O(n * k)
- **Space Complexity:** O(1)

### b. Optimized Time & Space Complexity
- **Time Complexity:** O(n)
- **Space Complexity:** O(1)

## 6. Conclusion
The sliding window technique efficiently reduces the need for redundant counting by only adjusting changes in the window. This approach is preferable for beginners to optimize problems involving contiguous substrings or fixed-length subarrays, providing both clarity and efficiency.
