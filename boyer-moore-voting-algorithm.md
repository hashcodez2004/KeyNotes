# 🗳️ Moore’s Voting Algorithm (Boyer–Moore Majority Vote)

### 📌 Definition
Find the **majority element** (value occurring **more than ⌊n/2⌋ times**) in an array in **O(n) time** and **O(1) space**.

> If a majority is **not guaranteed**, you must **verify** the candidate with a second pass.

---

### 🎯 Problem
Given `nums`, return the element that appears more than `n/2` times (assume it exists).

---

### 💡 Intuition
- Keep a **candidate** and a **count**.
- When you see the same element, **increment** count; otherwise **decrement**.
- If count hits 0, **switch** the candidate to the current element.
- Majority element survives all cancellations.

---

### 🛠 Algorithm (n/2 case)
1. `candidate = None`, `count = 0`
2. For each `x` in `nums`:
   - If `count == 0`: `candidate = x`
   - If `x == candidate`: `count++` else `count--`
3. (If majority not guaranteed) verify by counting occurrences of `candidate`.

---

### 📜 C++ Code (n/2 case)
```cpp
int majorityElement(vector<int>& nums) {
    int candidate = 0, count = 0;
    for (int x : nums) {
        if (count == 0) candidate = x;
        count += (x == candidate) ? 1 : -1;
    }
    // Optional verify if not guaranteed:
    // int freq = count_if(nums.begin(), nums.end(), [&](int v){ return v == candidate; });
    // if (freq <= nums.size()/2) throw runtime_error("No majority");
    return candidate;
}
```

---

### ⏱ Complexity
- **Time:** `O(n)` (single pass, plus optional `O(n)` verify)
- **Space:** `O(1)`

---

### ⚠️ Edge Cases / Notes
- Works even with **negatives/duplicates**.
- If majority **may not exist**, do a **second pass** to confirm.
- Not stable; does not give frequency by itself (needs another pass).

---

## ✨ Extension: Elements Appearing More Than ⌊n/3⌋ (Boyer–Moore II)
At most **two** such elements. Keep **two candidates** and their counts.

✅ We ensure that we don’t overwrite both candidates with the same element(can be treated as an edge case for this problem).

### 📜 C++ Code (n/3 case)
```cpp
vector<int> majorityElement(vector<int> v) {
    int n = v.size(); //size of the array

    int cnt1 = 0, cnt2 = 0; // counts
    int el1 = INT_MIN; // element 1
    int el2 = INT_MIN; // element 2

    // applying the Extended Boyer Moore's Voting Algorithm:
    for (int i = 0; i < n; i++) {
        if (cnt1 == 0 && el2 != v[i]) {
            cnt1 = 1;
            el1 = v[i];
        }
        else if (cnt2 == 0 && el1 != v[i]) {
            cnt2 = 1;
            el2 = v[i];
        }
        else if (v[i] == el1) cnt1++;
        else if (v[i] == el2) cnt2++;
        else {
            cnt1--, cnt2--;
        }
    }

    vector<int> ls; // list of answers

    // Manually check if the stored elements in
    // el1 and el2 are the majority elements:
    cnt1 = 0, cnt2 = 0;
    for (int i = 0; i < n; i++) {
        if (v[i] == el1) cnt1++;
        if (v[i] == el2) cnt2++;
    }

    int mini = int(n / 3) + 1;
    if (cnt1 >= mini) ls.push_back(el1);
    if (cnt2 >= mini) ls.push_back(el2);

    // Uncomment the following line
    // if it is told to sort the answer array:
    // sort(ls.begin(), ls.end()); //TC --> O(2*log2) ~ O(1);

    return ls;
}
```

### ⏱ Complexity (n/3 case)
- **Time:** `O(n)` + `O(n)` verify
- **Space:** `O(1)` Because O(2Log2) is as good as constant

---

### 🧠 When to Use
- Majority element guaranteed → **single pass** is enough.
- Majority not guaranteed → **add verification pass**.
- Need > n/3 elements → use **two-candidate** version.
