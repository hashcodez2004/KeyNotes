# 🔄 Types of Array Rotation
**📅 Date:** 2025-08-15  

---

## 1️⃣ Left Rotation
- **Definition:** Move each element to the left by `d` positions.
- **Example:**  
  Input: `[1, 2, 3, 4, 5]`, `d = 2`  
  Step-by-step:  
  1. Move `1` to end → `[2, 3, 4, 5, 1]`  
  2. Move `2` (new first element) to end → `[3, 4, 5, 1, 2]`
- **Result:** `[3, 4, 5, 1, 2]`

---

## 2️⃣ Right Rotation
- **Definition:** Move each element to the right by `d` positions.
- **Example:**  
  Input: `[1, 2, 3, 4, 5]`, `d = 2`  
  Step-by-step:  
  1. Move `5` to front → `[5, 1, 2, 3, 4]`  
  2. Move `4` (new last element) to front → `[4, 5, 1, 2, 3]`
- **Result:** `[4, 5, 1, 2, 3]`

---

## ⚖️ Key Differences

| Feature         | Left Rotation                | Right Rotation               |
|-----------------|------------------------------|------------------------------|
| Shift Direction | Towards start (index ↓)      | Towards end (index ↑)        |
| First element   | Goes to end                  | Comes from end               |
| Example Move    | `[1, 2, 3]` → `[2, 3, 1]`    | `[1, 2, 3]` → `[3, 1, 2]`    |

---

## 📌 Quick Tip
> Left rotation by `d` is the same as right rotation by `(n - d)` and vice versa.
