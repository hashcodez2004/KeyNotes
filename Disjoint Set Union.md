# Disjoint Set Union (DSU) / Union Find

## What is DSU?

A **Disjoint Set Union (DSU)**, also known as **Union Find**, is a data structure used to efficiently maintain multiple **disjoint (non-overlapping)** sets.

It mainly supports two operations:

- **Find** → Returns the representative (ultimate parent/root) of a node.
- **Union** → Merges two different sets into one.

---

# Representative (Ultimate Parent)

The **representative** of a set is the **root** of that set.

A node is the representative if:

```cpp
parent[node] == node;
```

Always use:

```cpp
findUPar(node);
```

Never assume:

```cpp
parent[node];
```

because `parent[node]` may only be the **immediate parent**, not the **ultimate parent (representative)**.

---

# Path Compression

## Idea

Whenever `find()` is called, every visited node is directly connected to the root.

Before:

```text
1 → 2 → 3 → 4 → 5
```

After `find(1)`:

```text
1 ─┐
2 ─┤
3 ─┤──► 5
4 ─┘
```

Future `find()` operations become much faster.

Implementation:

```cpp
int findUPar(int node) {
    if (parent[node] == node)
        return node;

    return parent[node] = findUPar(parent[node]);
}
```

### Path Compression is...

- Reactive optimization.
- Flattens an already tall tree.
- Does **not** prevent tall trees from being formed.

---

# Union by Rank

## What is Rank?

Rank is an approximation of the **height** of a tree.

Initially,

```cpp
rank = 0;
```

## Rule

- Attach the smaller-rank tree below the larger-rank tree.
- If both ranks are equal:
  - Attach either one.
  - Increase the new root's rank by **1**.

### Why?

Keeps the tree shallow, making `find()` operations faster.

---

# Union by Size

## What is Size?

Size represents the **number of nodes** in a connected component.

Initially,

```cpp
size = 1;
```

## Rule

Always attach the **smaller component** below the **larger component**.

Update the size of the new root.

Example:

```text
Size = 3      Size = 7

Merge

↓

Size = 10
```

---

# Why Use Both?

## Union by Rank / Size

- Prevents tall trees from forming.
- Proactive optimization.

## Path Compression

- Flattens existing tall trees.
- Reactive optimization.

### Easy Way to Remember

> **Union by Rank/Size prevents the problem.**  
> **Path Compression fixes the problem.**

Using both together gives the best practical performance.

---

# Time Complexities

| Technique | Worst Case | Amortized |
|-----------|-----------:|----------:|
| No Optimization | **O(n)** | **O(n)** |
| Path Compression Only | **O(n)** | **≈ O(log n)** |
| Union by Rank Only | **O(log n)** | **O(log n)** |
| Union by Size Only | **O(log n)** | **O(log n)** |
| Path Compression + Rank/Size | **O(n)** (single operation) | **O(α(n))** |

## Inverse Ackermann Function

`α(n)` is the **Inverse Ackermann Function**.

It grows extremely slowly.

For every practical value of `n`,

```text
α(n) < 5
```

Hence, DSU operations are considered **almost O(1)** in practice.

---

# Interview Notes

- DSU maintains multiple connected components.
- Every component has one representative (root).
- `find()` returns the representative.
- `union()` merges two different components.
- Path Compression optimizes `find()`.
- Union by Rank/Size optimizes `union()`.
- Together they provide an amortized complexity of **O(α(n))**, which is practically constant.

---

# Common Applications

- Kruskal's Minimum Spanning Tree (MST)
- Cycle Detection in Undirected Graph
- Number of Connected Components
- Number of Provinces
- Accounts Merge
- Most Stones Removed with Same Row or Column
- Dynamic Connectivity Problems
- Network Connectivity
- Offline Graph Queries
- Connected Component Queries

---

# Quick Revision

- **Representative = Root**
- Always use `findUPar()` before union.
- Path Compression → Flattens the tree.
- Union by Rank → Uses tree height.
- Union by Size → Uses component size.
- Rank/Size prevents tall trees.
- Path Compression flattens tall trees.
- Best Complexity = **O(α(n))** (amortized).
