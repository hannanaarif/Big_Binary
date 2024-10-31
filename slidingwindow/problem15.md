

# Problem Name: Count Substrings That Satisfy K-Constraint I

## 1.Problem Statement
You are given a binary string `s` and an integer `k`.

A binary string satisfies the k-constraint if either of the following conditions holds:
- The number of `0`s in the string is at most `k`.
- The number of `1`s in the string is at most `k`.

Return an integer denoting the number of substrings of `s` that satisfy the k-constraint.

## 2.Example Inputs:
- **Example 1:**
- **Input:** `s = "10101"`, `k = 1`
- **Output:** `12`
- **Explanation:** Every substring of `s` except the substrings "1010", "10101", and "0101" satisfies the k-constraint.

-**Example 2:**
- **Input:** `s = "1010101"`, `k = 2`
- **Output:** `25`
- **Explanation:** Every substring of `s` except the substrings with a length greater than 5 satisfies the k-constraint.

-**Example 3:**
- **Input:** `s = "11111"`, `k = 1`
- **Output:** `15`
- **Explanation:** All substrings of `s` satisfy the k-constraint.

## 3.Constraints
- `1 <= s.length <= 50`
- `1 <= k <= s.length`
- `s[i]` is either `'0'` or `'1'`.

---

## 4.Brute Force Approach

### a.Approach
1. Use a nested loop to iterate through all possible substrings of the binary string `s`.
2. For each substring, count the number of `0`s and `1`s.
3. If either the count of `0`s or `1`s is less than or equal to `k`, consider it as satisfying the constraint.

### b.Steps
1. Start with an empty count for substrings satisfying the k-constraint.
2. For each substring, check the number of `0`s and `1`s.
3. If either count is at most `k`, increment the count.

### c.Time and Space Complexity
- **Time Complexity:** `O(n^3)`, where `n` is the length of `s`, due to the substring generation and counting steps.
- **Space Complexity:** `O(1)` for auxiliary space, as we only use a few counters.

### d.Code Snippet
```javascript
function countKConstraintSubstringsBruteForce(s, k) {
  let count = 0;
  for (let i = 0; i < s.length; i++) {
    for (let j = i + 1; j <= s.length; j++) {
      let substring = s.slice(i, j);
      let zeroCount = (substring.match(/0/g) || []).length;
      let oneCount = (substring.match(/1/g) || []).length;
      if (zeroCount <= k || oneCount <= k) count++;
    }
  }
  return count;
}
```

### e.Dry Run
#### Input: `s = "10101"`, `k = 1`
1. All substrings are checked. 
2. Substrings "1010", "10101", and "0101" are identified as not satisfying the k-constraint.

---

## 5.Efficient Approach

### a.Approach (Sliding Window)
1. Use two pointers to create a sliding window for substrings.
2. For each window, maintain a count of `0`s and `1`s.
3. Expand or contract the window to maintain the counts such that either `0`s or `1`s stay below or equal to `k`.

### b.Steps
1. Initialize left and right pointers.
2. Expand the window by moving the right pointer and updating `0` and `1` counts.
3. If either count exceeds `k`, slide the left pointer to reduce the window size and adjust the counts.
4. Count substrings within the valid window sizes.

### c.Time and Space Complexity
- **Time Complexity:** `O(n)`, where `n` is the length of `s`, due to the single-pass sliding window.
- **Space Complexity:** `O(1)` for auxiliary space, as only counters are used.

### d.Code Snippet
```javascript
function countKConstraintSubstringsEfficient(s, k) {
  let count = 0;
  let zeroCount = 0, oneCount = 0;
  let left = 0;

  for (let right = 0; right < s.length; right++) {
    if (s[right] === '0') zeroCount++;
    else oneCount++;

    while (zeroCount > k && oneCount > k) {
      if (s[left] === '0') zeroCount--;
      else oneCount--;
      left++;
    }
    count += (right - left + 1);
  }
  return count;
}
```

### e.Dry Run
#### Input: `s = "10101"`, `k = 1`
1. Using sliding window, move the pointers and update counts to keep valid substrings.
2. Count all valid windows.

---

## 6.Complexity Analysis

### Brute Force
- **Time Complexity:** `O(n^3)`
- **Space Complexity:** `O(1)`

### Optimized
- **Time Complexity:** `O(n)`
- **Space Complexity:** `O(1)`

---

## Conclusion
This guide illustrates the significant difference between brute force and efficient solutions. The sliding window approach optimizes the solution by reducing the time complexity from `O(n^3)` to `O(n)`, making it feasible for larger inputs within the given constraints.
