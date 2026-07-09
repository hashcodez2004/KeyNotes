# BST Iterator — Complete Notes

## What is a BST Iterator?

A **BST Iterator** is **not a new data structure**.

It is simply an implementation of **Lazy Inorder Traversal**.

Instead of computing the complete inorder traversal and storing all `N` nodes, it generates the **next smallest element only when required**.

Think of it as an iterator over a sorted array.

---

# Core Idea

Traditional approach:

```
BST
   │
   ▼
Complete Inorder Traversal
   │
   ▼
Store all N elements in a vector
   │
   ▼
Process them
```

BST Iterator:

```
BST
   │
   ▼
Maintain only the current root-to-leaf path
   │
   ▼
Return one element at a time
```

Instead of storing all elements, it stores only the nodes required to generate the **next inorder element**.

---

# Space Complexity

Suppose the BST height is `H`.

Traditional inorder:

- Time : `O(N)`
- Space : `O(N)` (vector)

BST Iterator:

- Time (Construction): `O(H)`
- Time (`next()`): `O(1)` **amortized**
- Space: `O(H)`

---

# How does it work?

Initially,

```
pushAllLeft(root)
```

Example:

```
        5
       / \
      3   7
     / \
    2   4
```

Initially the stack contains

```
5
3
2
```

Top of stack = `2`

Calling

```
next()
```

returns

```
2
```

Then

- Pop `2`
- Push all left nodes of `2->right`

Since `2->right == NULL`, nothing is pushed.

Next stack

```
5
3
```

Next call returns

```
3
```

Now push all left nodes of

```
3->right
```

which pushes

```
4
```

Stack

```
5
4
```

This continues until all nodes are visited.

---

# Why is it called "Lazy"?

Because we don't compute everything in advance.

Instead of

```
Generate 100000 elements

↓

Use them
```

we do

```
Generate first element

↓

Use it

↓

Generate second element

↓

Use it

↓

...
```

The traversal is performed **on demand**.

---

# Complete Iterator Implementation

```cpp
class BSTIterator {
private:
    stack<TreeNode*> myStack;

public:
    BSTIterator(TreeNode *root) {
        pushAll(root);
    }

    bool hasNext() {
        return !myStack.empty();
    }

    int next() {
        TreeNode* tmpNode = myStack.top();
        myStack.pop();

        pushAll(tmpNode->right);

        return tmpNode->val;
    }

private:
    void pushAll(TreeNode* node) {
        while(node != NULL){
            myStack.push(node);
            node = node->left;
        }
    }
};
```

---

# Why did Striver create a separate class?

Without BST Iterator, every problem would require writing

- Stack
- Push all left nodes
- Pop
- Push left chain of right subtree

again and again.

Instead, Striver encapsulated this logic into a reusable class.

Now every problem becomes

```cpp
BSTIterator it(root);

while(it.hasNext()){
    cout << it.next();
}
```

The iterator hides all implementation details.

---

# Where have I already used this logic?

While solving **Merge Two BSTs**, I used **two stacks**.

At that time, I thought I was implementing a completely different algorithm.

Actually,

**I was implementing two independent BST Iterators.**

```
BST 1
   │
Iterator 1

BST 2
   │
Iterator 2
```

Then I simply merged both sorted streams exactly like merging two sorted arrays.

So,

> **Merge Two BSTs using two stacks is simply an application of the BST Iterator concept.**

The only difference is that Striver encapsulates the logic inside a reusable class.

---

# Where should BST Iterator come to mind?

Whenever the problem says

> **Give me elements one by one in sorted order.**

Instead of

```
Store inorder into vector
```

think

```
BST Iterator
```

---

# Common Applications

## 1. BST Traversal

Instead of

```
Vector
```

use

```
BST Iterator
```

---

## 2. Kth Smallest Element

Don't generate the complete inorder traversal.

Simply call

```
next()
```

`k` times.

---

## 3. Merge Two BSTs

Use

- Iterator 1
- Iterator 2

Merge exactly like merging two sorted arrays.

Space reduces from

```
O(N)
```

to

```
O(H1 + H2)
```

---

## 4. Two Sum in BST (Optimal)

Need

- Smallest element
- Largest element

Use

- Forward BST Iterator (Inorder)
- Reverse BST Iterator (Reverse Inorder)

Exactly like

```
left++
right--
```

on a sorted array.

Space

```
O(H)
```

instead of

```
O(N)
```

---

## 5. Streaming Large BSTs

Suppose BST contains

```
10 million nodes
```

Instead of storing all values,

consume them one at a time.

BST Iterator is ideal.

---

# Mental Trigger

Whenever you write

```cpp
vector<int> inorder;

inorderTraversal(root, inorder);
```

Pause for a second and ask

> **Do I really need the complete inorder traversal stored?**

If the answer is

> **No, I only need the next smallest element one by one.**

Think

> **BST Iterator**

---

# Important Insight

BST Iterator is **not another traversal**.

It is simply

```
Recursive Inorder

↓

Replace recursion with a stack

↓

Encapsulate the stack

↓

BST Iterator
```

---

# Time Complexities

| Operation | Complexity |
|-----------|-----------:|
| Construction | `O(H)` |
| `next()` | `O(1)` amortized |
| `hasNext()` | `O(1)` |
| Auxiliary Space | `O(H)` |

where

```
H = Height of BST
```

---

# One-Line Rule to Remember

> **Whenever I need sorted BST elements one at a time (instead of all at once), I should think of a BST Iterator rather than storing the complete inorder traversal.**
