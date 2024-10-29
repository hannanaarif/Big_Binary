
# Longest Nice Substring Guide

## 1. Problem Statement
A string `s` is "nice" if, for every letter of the alphabet that `s` contains, it appears both in uppercase and lowercase. For example, `"abABB"` is nice because both `'A'` and `'a'` appear, and `'B'` and `'b'` appear. However, `"abA"` is not because `'b'` appears, but `'B'` does not.

Given a string `s`, return the longest substring of `s` that is nice. If there are multiple, return the substring of the earliest occurrence. If there are none, return an empty string.

### Constraints:
- `1 <= s.length <= 100`
- `s` consists of uppercase and lowercase English letters.

## 2. Example Inputs and Outputs

- **Example 1:**
    - Input: `s = "YazaAay"`
    - Output: `"aAa"`
    - Explanation: `"aAa"` is a nice substring because `'A'` and `'a'` appear together, and it is the longest nice substring.

- **Example 2:**
    - Input: `s = "Bb"`
    - Output: `"Bb"`
    - Explanation: `"Bb"` is a nice substring because both `'B'` and `'b'` appear.

- **Example 3:**
    - Input: `s = "c"`
    - Output: `""`
    - Explanation: No nice substrings exist.

## 3. Brute Force Approach

### a. Approach
The brute-force approach involves generating all possible substrings of `s` and checking if each substring is "nice".

### b. Steps
1. Loop through each starting index of the string.
2. For each starting index, generate every possible substring ending at a later index.
3. For each substring, check if it is "nice" by verifying that each character in the substring has both uppercase and lowercase forms present.
4. Keep track of the longest "nice" substring found.

### c. Time & Space Complexity
- **Time Complexity:** O(n^3), due to the nested loops and checks for each substring.
- **Space Complexity:** O(n), for storing substrings.

### d. Code Snippet

```javascript
function longestNiceSubstring(s) {
    let longestNice = "";

    for (let i = 0; i < s.length; i++) {
        for (let j = i + 1; j <= s.length; j++) {
            const substr = s.slice(i, j);
            if (isNice(substr) && substr.length > longestNice.length) {
                longestNice = substr;
            }
        }
    }
    return longestNice;
}

function isNice(sub) {
    const set = new Set(sub);
    for (const char of set) {
        if (!set.has(char.toLowerCase()) || !set.has(char.toUpperCase())) {
            return false;
        }
    }
    return true;
}
```

### e. Dry Run
- Input: `s = "YazaAay"`
- Output: `"aAa"` after evaluating all substrings and verifying which is "nice".

## 4. Efficient Approach (Sliding Window)

### a. Approach
The sliding window approach reduces the need to check every possible substring individually. This is done by adjusting the window size dynamically based on conditions of the "niceness".

### b. Steps
1. Create a sliding window starting from index `0`.
2. Expand the window by moving the end pointer and checking if the current substring is nice.
3. If not, adjust the window by moving the starting pointer to find the next possible "nice" substring.
4. Track the longest "nice" substring.

### c. Time & Space Complexity
- **Time Complexity:** O(n^2), as we adjust the window and check subsets of the string.
- **Space Complexity:** O(n), for storing subsets.

### d. Code Snippet

```javascript
function longestNiceSubstring(s) {
    if (s.length < 2) return "";

    for (let len = s.length; len > 0; len--) {
        for (let i = 0; i + len <= s.length; i++) {
            const substr = s.slice(i, i + len);
            if (isNice(substr)) {
                return substr;
            }
        }
    }
    return "";
}
```

### e. Dry Run
- Input: `s = "YazaAay"`
- Start checking substrings from the longest possible and return `"aAa"` once found.

## 5. Complexity Analysis

### a. Brute Force Time & Space Complexity
- **Time Complexity:** O(n^3)
- **Space Complexity:** O(n)

### b. Optimized Time & Space Complexity
- **Time Complexity:** O(n^2)
- **Space Complexity:** O(n)

## 6. Conclusion
The sliding window technique optimizes the brute-force approach by dynamically adjusting the window size, reducing redundant checks. This guide compared brute-force and efficient approaches, explaining the trade-offs in complexity and the resulting improvements.
