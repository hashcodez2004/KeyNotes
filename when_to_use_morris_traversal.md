# Morris Traversal — Complete Notes

## What is Morris Traversal?

Morris Traversal is a technique to traverse a binary tree **without using recursion or an explicit stack**.

- **Time Complexity:** `O(N)`
- **Auxiliary Space:** `O(1)`

It achieves this by temporarily modifying the tree (creating **threads**) and restoring it before finishing, so the original tree remains unchanged.

---

# The Core Idea

Normally, recursion or a stack is required because after exploring a subtree, we need a way to return to its parent.

Morris Traversal eliminates this need by creating temporary links.

Instead of remembering the parent in a stack, it temporarily connects:

- **Inorder:** predecessor → current
- **Reverse Inorder:** successor → current

Once the traversal returns, the temporary link is removed.

---

# When Should You Think of Morris Traversal?

Ask yourself:

> **Can this problem be solved simply by visiting nodes in a particular order?**

If the answer is **YES**, Morris may be applicable.

If the problem requires information to be returned from child nodes to the parent, Morris is usually **not** the correct choice.

---

# Morris is NOT a New Traversal

Morris is **not** another traversal like preorder or inorder.

It is only a different implementation of DFS traversals.

Think of it as:

> **Recursion/Stack Replacement Technique**

Instead of

- Recursion
- Explicit Stack

it uses

- Temporary Threads

---

# Mental Model

Tree traversal can be done using

```
Traversal Order
        │
        ▼
Recursion
Stack
Morris
```

The traversal order remains the same.

Only the implementation changes.

---

# Traversals Supported by Morris

## 1. Inorder

```
Left → Root → Right
```

Applications:

- BST Validation
- Kth Smallest
- Recover BST
- Inorder Traversal

---

## 2. Reverse Inorder

```
Right → Root → Left
```

Applications:

- Kth Largest
- Descending BST Traversal

---

## 3. Preorder

```
Root → Left → Right
```

Can also be implemented using Morris.

---

## Postorder?

Possible, but considerably more complicated.

It is rarely expected in interviews.

---

# When Does Morris Work?

Morris works when the algorithm only needs to **visit nodes**.

Typical examples:

- Inorder Traversal
- BST Validation
- Kth Smallest
- Kth Largest
- Recover BST
- Printing nodes
- Counting nodes
- Searching while traversing

Notice the common pattern:

> We only process nodes when they are visited.

No information needs to be returned from children.

---

# When Morris Does NOT Work

Morris is generally **not suitable** for problems requiring results from subtrees.

Examples:

- Height of Tree
- Diameter
- Balanced Binary Tree
- Maximum Path Sum
- Largest BST
- Lowest Common Ancestor (General Binary Tree)
- Tree DP problems

These problems require child results before computing the parent's answer.

Example:

```cpp
height(root) =
1 + max(height(left), height(right));
```

The parent depends on information coming back from both children.

Morris cannot naturally provide this.

---

# Easy Recognition Rule

If your recursive function looks like

```cpp
int solve(TreeNode* root)
```

or

```cpp
NodeInfo solve(TreeNode* root)
```

or

```cpp
pair<int,int> solve(TreeNode* root)
```

you're probably solving a **postorder/DP problem**, not a Morris problem.

---

# Decision Tree

```
Does the problem only require visiting nodes?
        │
       Yes
        │
        ▼
Which traversal solves it?

        │
        ▼
Can recursion solve it?
        │
       Yes
        │
        ▼
Need O(1) extra space?
        │
      Yes
        │
        ▼
Think Morris Traversal
```

---

# Another Decision Tree

```
Does the parent require information
from its children?

        │
      Yes
        │
        ▼
Use Postorder Recursion

NOT Morris
```

---

# Reverse Morris Traversal

Reverse Morris is simply the mirror image of Morris Inorder.

Instead of

```
Left → Root → Right
```

it performs

```
Right → Root → Left
```

Changes:

- Go right instead of left.
- Find inorder successor instead of predecessor.
- Create thread:
  successor → current

Applications:

- Kth Largest
- Descending BST Traversal

---

# Interview Strategy

When solving a tree problem, think in this order:

### Step 1

What traversal naturally solves the problem?

---

### Step 2

Implement it recursively.

---

### Step 3

Need iterative?

Use a stack.

---

### Step 4

Need `O(1)` auxiliary space?

Think Morris Traversal.

---

# Important Insight

Morris is an **optimization technique**, not a problem-solving technique.

It changes

```
Recursion
```

into

```
Temporary Threads
```

without changing the traversal order or the algorithm itself.

---

# Summary Table

| Problem Type | Morris? |
|--------------|---------|
| Inorder Traversal | ✅ |
| Preorder Traversal | ✅ |
| Reverse Inorder | ✅ |
| BST Validation | ✅ |
| Recover BST | ✅ |
| Kth Smallest | ✅ |
| Kth Largest | ✅ |
| Count Nodes During Traversal | ✅ |
| Search While Traversing | ✅ |
| Height of Tree | ❌ |
| Diameter | ❌ |
| Balanced Tree | ❌ |
| Maximum Path Sum | ❌ |
| Largest BST | ❌ |
| LCA (General Tree) | ❌ |
| Tree DP Problems | ❌ |

---

# One-Line Rule to Remember

> **If the problem only needs you to _visit_ nodes in a specific DFS order, Morris may replace recursion or a stack. If the problem needs information to _flow back_ from children to parents, Morris is generally not the right tool.**
