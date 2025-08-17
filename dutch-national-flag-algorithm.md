# 🇳🇱 Dutch National Flag Algorithm

### 📌 Definition

-   Algorithm by **Edsger Dijkstra**.
-   Efficient way to sort an array of **3 distinct elements** (e.g.,
    `0, 1, 2`).
-   Works in **O(n) time** and **O(1) space**.

------------------------------------------------------------------------

### 🎯 Problem Statement

Given an array with only `0s`, `1s`, and `2s`, sort it in-place:

    Input  : [2,0,2,1,1,0]
    Output : [0,0,1,1,2,2]

------------------------------------------------------------------------

### 🛠 Idea

Maintain three pointers: - `low` → boundary for 0s - `mid` → current
element - `high` → boundary for 2s

Rules: - If `arr[mid] == 0`: swap `arr[low]` & `arr[mid]`; increment
both `low`, `mid`. - If `arr[mid] == 1`: just increment `mid`. - If
`arr[mid] == 2`: swap `arr[mid]` & `arr[high]`; decrement `high`.

------------------------------------------------------------------------

### 📜 C++ Code

``` cpp
void sortColors(vector<int>& nums) {
    int low = 0, mid = 0, high = nums.size() - 1;

    while (mid <= high) {
        if (nums[mid] == 0) swap(nums[low++], nums[mid++]);
        else if (nums[mid] == 1) mid++;
        else swap(nums[mid], nums[high--]);
    }
}
```

------------------------------------------------------------------------

### ⏱ Complexity

-   **Time:** `O(n)` (single pass)
-   **Space:** `O(1)` (in-place)

------------------------------------------------------------------------

### 🔎 Applications

-   Sorting 0s, 1s, 2s (Leetcode 75: *Sort Colors*).
-   Partition arrays into 3 groups (e.g., negatives, zeros, positives).
-   Basis for **3-way partitioning in quicksort**.
