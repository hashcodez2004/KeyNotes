# Subarray, Subsequence, Subset – Quick Notes

## Subarray
- Contiguous part of array.
- Empty not counted.
- Formula: n(n+1)/2

---

## Subsequence
- Not necessarily contiguous, order preserved.
- Empty subsequence:
  - Included → 2^n
  - Excluded → 2^n - 1

---

## Subset
- Any combination of elements, order doesn’t matter.
- Empty always included.
- Formula: 2^n

---

## Comparison

| Concept     | Contiguous? | Order Matters? | Empty Included?         | Formula              |
|-------------|-------------|----------------|-------------------------|----------------------|
| Subarray    | ✅ Yes      | ✅ Yes         | ❌ No                   | n(n+1)/2             |
| Subsequence | ❌ No       | ✅ Yes         | Convention (Yes / No)   | 2^n / (2^n - 1)      |
| Subset      | ❌ No       | ❌ No          | ✅ Yes                  | 2^n                  |
