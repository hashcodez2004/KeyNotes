# Recursion Patterns Cheat Sheet

## 1. Take / Not Take (Binary Choice)
- Each element → either **pick** or **skip**.
- Used for **subsequence-style** problems.
- Examples:
  - Generate all subsequences
  - Subsequence sum = K
  - Check if subsequence exists

### Template:
```cpp
void helper(int idx, vector<int>& nums, vector<int>& ds) {
    if(idx == nums.size()) { /* process ds */ return; }
    // take
    ds.push_back(nums[idx]);
    helper(idx+1, nums, ds);
    ds.pop_back();
    // not take
    helper(idx+1, nums, ds);
}
```

---

## 2. For Loop + Recursion (Multiple Choices)
- At each step → try **all future choices**.
- Helps handle **combinations** and **duplicates**.
- Examples:
  - Subsets with duplicates
  - Combination Sum I & II
  - Generate k-combinations
  - N-Queens / Sudoku

### Template:
```cpp
void helper(int idx, vector<int>& nums, vector<int>& ds) {
    ans.push_back(ds); // store subset/combination
    for(int i = idx; i < nums.size(); i++) {
        if(i > idx && nums[i] == nums[i-1]) continue; // skip duplicates
        ds.push_back(nums[i]);
        helper(i+1, nums, ds);
        ds.pop_back();
    }
}
```

---

### Rule of Thumb:
- **Binary decision for each index?** → Take/Not Take.  
- **Explore all future choices starting from this index?** → For Loop + Recursion.



## Handling Duplicates in Recursion Problems

- **Step 1:** Always sort the array first.
- **Step 2:** Skip duplicates at the same recursion level:
  - In a for loop:
    `if (i > idx && nums[i] == nums[i-1]) continue;`
- **Step 3:** This ensures unique results in problems like:
  - Subsets with duplicates
  - Combination Sum II
  - Unique permutations

👉 Rule of Thumb:  
Whenever you see “unique / no duplicates in output” → think **Sort + Skip Duplicates**.



# 📘 Recursion Base Case Patterns (Cheat Sheet)

## 🔑 Two Styles of Recursion
1. **Traversal-style** → base case when we *reach the end position or consume full input*.  
2. **Decision-style** → base case when we *fill all slots/choices successfully*.  

---

## 📝 Problem-wise Comparison

| Problem                  | Type              | What recursion processes? | Choices made                      | Base Case                 | Why here?                       | TC (worst case)      | SC                |
|--------------------------|-------------------|---------------------------|-----------------------------------|---------------------------|---------------------------------|----------------------|-------------------|
| **Rat in a Maze**        | Traversal         | Current cell (i,j)        | Move in 4 dirs (D,L,R,U)          | `if (i==n-1 && j==n-1)`   | Goal = reach destination cell   | O(4^(N^2))           | O(N^2) stack      |
| **Word Break**           | Traversal         | Current index in string   | Cut or not cut at next pos        | `if (idx==s.size())`      | Goal = consume entire string    | O(2^n) (no memo)     | O(n)              |
| **Palindrome Partition** | Traversal + Cut   | Current index in string   | Cut at palindromic substrings     | `if (idx==s.size())`      | Goal = fully partition string   | O(2^n * n)           | O(n)              |
| **N-Queens**             | Decision          | Current row               | Choose a safe column              | `if (row==n)`             | All rows got a queen            | O(N!)                | O(N^2) board+stack|
| **Graph Coloring**       | Decision          | Current node              | Choose safe color {1…m}           | `if (node==V)`            | All nodes colored               | O(m^V)               | O(V)              |
| **Sudoku Solver**        | Decision          | Current empty cell        | Place digit {1…9} if valid        | `if (row==9)`             | All cells filled                | O(9^(81)) worst-case | O(81) stack       |


## 🎯 Quick Rule of Thumb
- **Traversal-style** → Base case = "Have I reached the end?"  
- **Decision-style** → Base case = "Have I filled all slots/choices?"  

👉 Always identify whether recursion is **walking to an end** or **filling choices**. That tells you *where to return*.  


