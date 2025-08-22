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

