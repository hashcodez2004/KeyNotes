# Prefix Sum Algorithm

## 1. Introduction
The **Prefix Sum Algorithm** is a technique to preprocess an array so that range sum queries can be answered efficiently.  
It is widely used in problems involving cumulative sums and subarray computations.

---

## 2. Concept
- Given an array `arr[0..n-1]`, the prefix sum array `prefix[i]` stores the sum of elements from `arr[0]` to `arr[i]`.
  
  **Formula:**  
  ```
  prefix[0] = arr[0]
  prefix[i] = prefix[i-1] + arr[i]   (for i > 0)
  ```

- With this, the sum of any subarray `arr[l..r]` can be computed as:
  ```
  sum(l, r) = prefix[r] - prefix[l-1]   (if l > 0)
  sum(l, r) = prefix[r]                 (if l == 0)
  ```

---

## 3. Steps to Use
1. Build the prefix sum array in `O(n)` time.  
2. Answer range sum queries in `O(1)` time using the formula.  

---

## 4. Example

### Input
```
arr = [2, 4, 6, 8, 10]
```
### Prefix Sum Array
```
prefix = [2, 6, 12, 20, 30]
```

### Query Example
- Sum from index `1` to `3` (subarray `[4, 6, 8]`):
```
sum(1,3) = prefix[3] - prefix[0] = 20 - 2 = 18
```

---

## 5. Time & Space Complexity
- **Prefix array construction:** `O(n)`  
- **Range sum query:** `O(1)`  
- **Space complexity:** `O(n)` (for prefix array)

---

Always watch out for **0-based indexing adjustments**.

---

✅ Prefix Sum is a fundamental tool for array range queries, reducing repeated summation work into a preprocessing + O(1) query model.
