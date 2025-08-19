# 📝 Merge Sort in Pair-Based Array Problems

## 🔑 Core Idea
- Merge Sort splits array → merges back in sorted order.  
- While merging, use sorted halves to **count pair conditions efficiently**.  
- Cuts down from `O(n²)` brute force → `O(n log n)`.

---

## ✅ When to Use
Use **Modified Merge Sort** when asked to **count pairs `(i, j)` with `i < j`** under conditions like:
- **Inversions** → `arr[i] > arr[j]`
- **Reverse Pairs** → `arr[i] > 2*arr[j]`
- Other variations → (`arr[i] + arr[j] > K`, `arr[i] < m*arr[j]`, etc.)

---

## 🚀 Why Merge Sort?
- Brute force: `O(n²)`  
- Merge Sort counting: `O(n log n)`  
- Alternative: BIT/Segment Tree (`O(n log n)` but harder to code).  
- Merge Sort = **clean + intuitive**.

---

## 📌 Key Takeaway
Whenever problem says:  
> “Count pairs `(i, j)` with `i < j` under some value-based condition”  

👉 Think **Modified Merge Sort**.  
