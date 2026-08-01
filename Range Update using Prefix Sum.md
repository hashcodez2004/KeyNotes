# Difference Array (Range Update Technique)

## Overview

The **Difference Array** is a powerful optimization technique used to perform **multiple range updates efficiently**.

Instead of updating every element inside a range, we only mark **where an update starts** and **where it ends**. After processing all updates, a single **prefix sum** converts the difference array into the final updated array.

---

# Official Name

- **Difference Array** ✅ (Most Common)
- **1D Difference Array**
- **Range Update using Prefix Sum**

---

# Intuition

Suppose we have an array:

```text
Index : 0 1 2 3 4 5
Value : 0 0 0 0 0 0
```

We receive the update:

> Add **5** to every element from index **1** to **4**.

### Normal Approach

```cpp
for(int i=l;i<=r;i++)
    arr[i]+=5;
```

Time Complexity:

```
O(length of range)
```

If there are many updates, complexity becomes

```
O(Number of Updates × Array Size)
```

which can be too slow.

---

# Difference Array Idea

Instead of updating every index, simply record:

- **Where the update starts**
- **Where the update stops**

For update

```text
[1,4] += 5
```

do

```cpp
diff[1] += 5;

if(r + 1 < n)
    diff[5] -= 5;
```

Difference Array becomes

```text
Index : 0 1 2 3 4 5
Diff  : 0 5 0 0 0 -5
```

Notice that this is **NOT** the final array.

---

# Recover Final Array

Take Prefix Sum.

```cpp
for(int i=1;i<n;i++)
    diff[i]+=diff[i-1];
```

Result

```text
Index : 0 1 2 3 4 5

Final : 0 5 5 5 5 0
```

Exactly what we wanted.

---

# Why Does It Work?

Think of updates as **events**.

```text
+5
```

means

> Start adding +5 from this index.

```text
-5
```

means

> Stop adding +5 after this point.

The prefix sum naturally carries the value until it gets cancelled.

---

# Another Example

Updates

```text
[2,5] += 10
[4,7] += 3
```

Instead of updating every element

Difference Array

```text
Index

0 1 2 3 4 5 6 7

Diff

0 0 10 0 3 0 -10 0
```

Take Prefix Sum

```text
0
0
10
10
13
13
3
3
```

Final Bonus Array

```text
0 0 10 10 13 13 3 3
```

---

# Generic Template

```cpp
vector<long long> diff(n+1,0);

for(auto &q: queries){

    int l=q[0];
    int r=q[1];
    long long val=q[2];

    diff[l]+=val;

    if(r+1<n)
        diff[r+1]-=val;
}

vector<long long> arr(n);

arr[0]=diff[0];

for(int i=1;i<n;i++)
    arr[i]=arr[i-1]+diff[i];
```

---

# Complexity

Let

```
n = Array Size

m = Number of Updates
```

Difference Array

```
Range Updates : O(m)

Prefix Sum    : O(n)

Total         : O(n+m)
```

Naive Method

```
O(n*m)
```

---

# Recognition Pattern

Whenever a problem says

> Perform many operations on intervals/ranges

such as

- Add X to every element in [L,R]
- Increase values on intervals
- Decrease values on intervals
- Apply boosts on segments
- Population change in cities
- Salary increment in departments
- Road construction on ranges
- Rainfall on intervals
- Damage/Healing on ranges

and finally asks

> What is the final value at every index?

Difference Array should immediately come to mind.

---

# When NOT to Use

Difference Array is **not suitable** if the problem asks

- Range Sum Queries after every update
- Point Queries after every update
- Intermixed Updates and Queries

Example

```
Update

Query

Update

Query

Update

Query
```

For these problems use

- Fenwick Tree (BIT)
- Segment Tree
- Segment Tree with Lazy Propagation

---

# Difference Array vs Prefix Sum

## Prefix Sum

Purpose

```
Fast Range Queries
```

Example

```
Many queries asking

Sum from L to R
```

Operation

```
Query becomes O(1)
```

Updates are expensive.

---

## Difference Array

Purpose

```
Fast Range Updates
```

Example

```
Many updates asking

Add X on L to R
```

Operation

```
Update becomes O(1)
```

Queries are answered after taking Prefix Sum once.

---

# Trick to Remember

Imagine painting a road.

Instead of painting every meter,

you put two signboards.

```
START PAINTING HERE (+X)

STOP PAINTING HERE (-X)
```

Then simply walk from left to right carrying the paint.

Whenever you see

```
+X
```

start painting.

Whenever you see

```
-X
```

stop painting.

That walk is exactly the Prefix Sum.

---

# Real Problems Using Difference Array

- LeetCode 370 — Range Addition
- Corporate Flight Bookings
- Car Pooling
- Brightness of Lamps
- Range Increment Problems
- Interval Addition Problems
- Competitive Programming Range Update Questions

---

# Related Techniques

| Technique | Purpose |
|-----------|---------|
| Prefix Sum | Fast Range Sum Queries |
| Difference Array | Fast Range Updates |
| Binary Search on Answer | Monotonic Problems |
| Sliding Window | Contiguous Subarrays |
| Two Pointers | Sorted Arrays / Pair Problems |
| Monotonic Stack | Next Greater/Smaller Element |
| Fenwick Tree (BIT) | Dynamic Prefix Queries |
| Segment Tree | Dynamic Range Queries |
| Lazy Propagation | Dynamic Range Updates |

---

# Key Takeaways

- Difference Array optimizes **multiple range updates**.
- Instead of updating every index:
  - Mark where an update **starts**.
  - Mark where an update **ends**.
- A single Prefix Sum reconstructs the final array.
- Complexity improves from

```
O(n*m)
```

to

```
O(n+m)
```

- One of the most frequently used techniques in Competitive Programming and DSA interviews.
