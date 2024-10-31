
# Problem Name: Maximum Length Substring With Two Occurrences

## 1. Problem Statement
You are given a string `s`. Find the length of the longest substring that contains at most two occurrences of each character.

### Example 1:
- Input: `s = "bcbbbcba"`
- Output: `4`
- Explanation: A valid substring with length `4` is `"bcbb"`, which contains each character at most twice.

### Example 2:
- Input: `s = "aaaa"`
- Output: `2`
- Explanation: A valid substring with length `2` is `"aa"`, which has each character at most twice.

## 2. Brute Force Approach

### a. Approach
- Explore all possible substrings and check if each satisfies the condition of having at most two occurrences per character.
- Track the length of the longest valid substring.

### b. Steps
1. Loop through each possible starting index `i`.
2. For each starting index, try to extend the substring by including characters until the condition of having at most two occurrences per character is broken.
3. Track the longest valid substring length.

### c. Time & Space Complexity
- **Time Complexity:** O(n^2), where `n` is the length of `s`, because we generate and check all substrings.
- **Space Complexity:** O(1) additional space.

### d. Code Snippet
```javascript
function maxLengthSubstringTwoOccurrences(s) {
  let maxLength = 0;

  for (let i = 0; i < s.length; i++) {
    const charCount = {};
    let valid = true;
    for (let j = i; j < s.length; j++) {
      charCount[s[j]] = (charCount[s[j]] || 0) + 1;
      if (charCount[s[j]] > 2) {
        valid = false;
        break;
      }
      if (valid) maxLength = Math.max(maxLength, j - i + 1);
    }
  }

  return maxLength;
}
```

### e. Dry Run
- For `s = "bcbbbcba"`, the longest substring with each character appearing at most twice is `"bcbb"` with a length of `4`.

## 3. Efficient Approach (Sliding Window)

### a. Approach
- Use a sliding window technique to keep track of the counts of each character within the window.
- If a character count exceeds `2`, move the starting pointer (`left`) forward to keep the window valid.

### b. Steps
1. Initialize two pointers, `left` and `right`, for the window and a map to count occurrences.
2. Expand `right` to add characters, updating their counts in the map.
3. If any character count goes above `2`, move `left` to reduce counts until the window is valid again.
4. Track the maximum valid window length.

### c. Time & Space Complexity
- **Time Complexity:** O(n), since each character is processed at most twice.
- **Space Complexity:** O(1), as only a fixed number of lowercase letters are tracked in the map.

### d. Code Snippet
```javascript
function maxLengthSubstringTwoOccurrences(s) {
  const charCount = {};
  let left = 0, maxLength = 0;

  for (let right = 0; right < s.length; right++) {
    charCount[s[right]] = (charCount[s[right]] || 0) + 1;

    while (charCount[s[right]] > 2) {
      charCount[s[left]]--;
      left++;
    }

    maxLength = Math.max(maxLength, right - left + 1);
  }

  return maxLength;
}
```

### e. Dry Run
- For `s = "aaaa"`, the sliding window adjusts to keep only two `a`s in the window, resulting in a maximum substring length of `2`.

## 4. Complexity Analysis

### a. Brute Force
- **Time Complexity:** O(n^2)
- **Space Complexity:** O(1)

### b. Optimized
- **Time Complexity:** O(n)
- **Space Complexity:** O(1)

## 5. Conclusion
- The brute force method is simple but slow, especially for longer strings.
- The sliding window approach improves efficiency by dynamically adjusting the window and updating counts, making it better suited for larger inputs.
