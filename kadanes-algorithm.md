# Kadane’s Algorithm – Intuition Notes ✨

## What are we solving?
We want the **maximum sum of a contiguous subarray**.  
👉 Example: `[−2, 1, −3, 4, −1, 2, 1, −5, 4]` → Answer = `6` (from `[4, −1, 2, 1]`).

---

## Key Intuition
- Imagine you are **walking through the array**, carrying a bag (`currSum`).
- At each step:
  - If adding the current number makes the bag **heavier in a good way** (positive gain) → keep it.
  - If the bag becomes **too heavy negatively (sum < 0)** → throw the bag away and start fresh from the next element.
- Along the walk, always note the **heaviest bag you carried** → that’s the max subarray sum.

---

## Why reset when sum < 0?
- A negative `currSum` will **drag down any future sum**.
- Better to start fresh at the next element → since adding a negative prefix can never help.

---

## Step-by-Step Thought Flow
1. `currSum` = best sum **ending at current index**.
2. `maxSum` = best sum **found so far**.
3. Update rule:  
   - Either **extend old subarray** (`currSum + x`)  
   - Or **start new at x**.

---

## Complexity
- **Time:** `O(n)` → one pass.
- **Space:** `O(1)` → only two variables.

---

## Quick Reminders
- Works with positives + negatives.
- If all numbers are negative → still gives the **largest (least negative) number**.

---

## Mental Picture 🧠
Kadane =  
- *"Grow the subarray as long as it helps me."*  
- *"Drop it the moment it hurts me."*
