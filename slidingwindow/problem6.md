
# Problem Name: Substrings of Size Three with Distinct Characters

## 1. Problem Statement
A string is considered "good" if there are no repeated characters. Given a string `s`, return the number of good substrings of length three in `s`.

Note that if there are multiple occurrences of the same substring, each occurrence should be counted.

A substring is a contiguous sequence of characters in a string.

### Constraints:
- `1 <= s.length <= 100`
- `s` consists of lowercase English letters.

## 2. Example Inputs and Outputs

- **Example 1:**
    - Input: `s = "xyzzaz"`
    - Output: `1`
    - Explanation: There are 4 substrings of size 3: `"xyz"`, `"yzz"`, `"zza"`, and `"zaz"`. The only good substring of length 3 is `"xyz"`.

- **Example 2:**
    - Input: `s = "aababcabc"`
    - Output: `4`
    - Explanation: There are 7 substrings of size 3: `"aab"`, `"aba"`, `"bab"`, `"abc"`, `"bca"`, `"cab"`, and `"abc"`. The good substrings are `"abc"`, `"bca"`, `"cab"`, and `"abc"`.

## 3. Brute Force Approach

### a. Approach
The brute-force approach involves generating all possible substrings of length 3 and checking if each substring contains only unique characters.

### b. Steps
1. Loop through each starting index of the string up to `s.length - 2`.
2. For each index, extract a substring of length 3.
3. Check if the substring has all unique characters.
4. Count each valid "good" substring.

### c. Time & Space Complexity
- **Time Complexity:** O(n), where `n` is the length of `s`.
- **Space Complexity:** O(1), for the substring storage.

### d. Code Snippet

```javascript
function countGoodSubstrings(s) {
    let count = 0;

    for (let i = 0; i < s.length - 2; i++) {
        const substr = s.slice(i, i + 3);
        if (isGood(substr)) {
            count++;
        }
    }
    return count;
}

function isGood(sub) {
    return sub[0] !== sub[1] && sub[1] !== sub[2] && sub[0] !== sub[2];
}
```

### e. Dry Run
- Input: `s = "xyzzaz"`
- Output: `1` after evaluating all substrings of length 3 and verifying which are "good".

## 4. Efficient Approach (Sliding Window)

### a. Approach
The sliding window approach allows for a more efficient solution by maintaining a window of size 3 and checking for uniqueness as the window slides.

### b. Steps
1. Initialize a window of size 3 at the start of `s`.
2. Check if all characters in the window are unique.
3. Slide the window one character to the right and repeat until the end of the string.
4. Count each valid "good" substring.

### c. Time & Space Complexity
- **Time Complexity:** O(n), as we only need to check each character once within the window.
- **Space Complexity:** O(1), for tracking characters in the window.

### d. Code Snippet

```javascript
function countGoodSubstrings(s) {
    let count = 0;

    for (let i = 0; i < s.length - 2; i++) {
        if (s[i] !== s[i + 1] && s[i + 1] !== s[i + 2] && s[i] !== s[i + 2]) {
            count++;
        }
    }
    return count;
}
```

### e. Dry Run
- Input: `s = "aababcabc"`
- Slide through each substring of size 3, count each substring like `"abc"`, `"bca"`, `"cab"`, and `"abc"` that has all distinct characters.

## 5. Complexity Analysis

### a. Brute Force Time & Space Complexity
- **Time Complexity:** O(n)
- **Space Complexity:** O(1)

### b. Optimized Time & Space Complexity
- **Time Complexity:** O(n)
- **Space Complexity:** O(1)

## 6. Conclusion
Both the brute-force and sliding window approaches offer linear time solutions. The sliding window approach, however, is conceptually simpler for checking fixed-size substrings and avoids extra storage by operating directly on the main string, providing a practical introduction to the sliding window technique for solving similar substring problems.
