
# Problem Name: Maximum Length Substring With Two Occurrences

## 1. Problem Statement
Given a string `s`, return the maximum length of a substring such that it contains at most two occurrences of each character.

## 2. Example Inputs
- **Example 1**:
  - **Input**: s = "bcbbbcba"
  - **Output**: 4
  - **Explanation**: The substring with maximum length that contains at most two occurrences of each character is "bcbb**bcba**".

- **Example 2**:
  - **Input**: s = "aaaa"
  - **Output**: 2
  - **Explanation**: The substring with maximum length that contains at most two occurrences of each character is "**aa**aa".

## 3. Brute Force Approach

### a. Approach
In this approach, we will consider every possible substring of `s` and check if it contains at most two occurrences of each character.

### b. Steps
1. Loop through all possible starting indices of substrings.
2. For each starting index, loop through each ending index to create substrings.
3. Check if the substring contains at most two occurrences of each character by counting occurrences.
4. Keep track of the maximum length of any valid substring.

### c. Time & Space Complexity
- **Time Complexity**: `O(n^3)` since we are generating all substrings and counting character occurrences for each substring.
- **Space Complexity**: `O(n)` for storing each substring.

### d. Code Snippet

```javascript
function maxLengthSubstringBruteForce(s) {
    let maxLength = 0;
    for (let i = 0; i < s.length; i++) {
        for (let j = i; j < s.length; j++) {
            let substring = s.slice(i, j + 1);
            let charCount = {};
            let valid = true;
            for (let char of substring) {
                charCount[char] = (charCount[char] || 0) + 1;
                if (charCount[char] > 2) {
                    valid = false;
                    break;
                }
            }
            if (valid) {
                maxLength = Math.max(maxLength, substring.length);
            }
        }
    }
    return maxLength;
}
```

### e. Dry Run
- **Input**: "bcbbbcba"
- Loop through all possible substrings and calculate character counts to find the maximum valid substring length.

## 4. Efficient Approach

### a. Approach (Sliding Window)
Use a sliding window approach to create a dynamic range (window) over the input string. This window will expand or shrink as we encounter characters to maintain at most two occurrences of each character.

### b. Steps
1. Use two pointers, `left` and `right`, where `right` expands the window by moving through the string.
2. For each new character at `right`, update its count.
3. If any character exceeds two occurrences, increment the `left` pointer to shrink the window until all characters have at most two occurrences.
4. Track the maximum length of the valid window throughout.

### c. Time & Space Complexity
- **Time Complexity**: `O(n)` as each character is processed only once.
- **Space Complexity**: `O(1)` as only fixed extra space is needed for counting.

### d. Code Snippet

```javascript
function maxLengthSubstringEfficient(s) {
    let left = 0;
    let maxLength = 0;
    let charCount = {};
    
    for (let right = 0; right < s.length; right++) {
        let char = s[right];
        charCount[char] = (charCount[char] || 0) + 1;
        
        while (charCount[char] > 2) {
            charCount[s[left]]--;
            left++;
        }
        
        maxLength = Math.max(maxLength, right - left + 1);
    }
    return maxLength;
}
```

### e. Dry Run
- **Input**: "bcbbbcba"
- Using a sliding window, adjust `left` pointer when counts exceed two, tracking the maximum window size with valid character counts.

## 5. Complexity Analysis

### a. Brute Force Time & Space Complexity
- **Time Complexity**: `O(n^3)`
- **Space Complexity**: `O(n)`

### b. Optimized Time and Space Complexity
- **Time Complexity**: `O(n)`
- **Space Complexity**: `O(1)`

## 6. Conclusion
The brute force approach provides a simple solution, but it's inefficient for larger strings. The sliding window technique improves efficiency significantly, making it the preferred method for problems requiring checks over dynamic ranges.
