# Choosing Between Recursion, Graph, and DP

## 🔹 Recursion / Backtracking
- Used when the task requires **exploring all possible configurations or paths**.  
- Suitable when input size is **small** or when **every possibility must be generated**.  
- Works well when **no overlapping subproblems** exist.  
- Typically involves **choice-making** at each step and exploring both "take" and "not-take" branches.  

---

## 🔹 Graph Traversal (DFS/BFS)
- Applied when the problem can be **represented as nodes and edges** (explicitly or implicitly).  
- Suitable for exploring **connectivity, reachability, or shortest path**.  
- Used when each state or position is **unique and not revisited often**, so memoization is not necessary.  
- Often implemented with **DFS, BFS, or Dijkstra** depending on requirements.  

---

## 🔹 Dynamic Programming (DP)
- Applied when there are **overlapping subproblems** (same state is solved multiple times).  
- Suitable when the task involves **optimization (min/max)** or **counting distinct ways**.  
- Transforms recursive exploration into a **memoized or tabulated** solution for efficiency.  
- Turns exponential recursion into **polynomial time**.  

---

## 🔹 How to Decide
1. **Is the task about generating or exploring all possible outcomes?**  
   → Use **Recursion/Backtracking**.  

2. **Can the task be modeled as moving between connected states or positions?**  
   → Use **Graph Traversal (DFS/BFS)**.  

3. **Do you encounter repeated subproblems or need optimization/counting?**  
   → Use **Dynamic Programming**.  

---

✅ **Rule of Thumb**:  
- Graph structure → **DFS/BFS**  
- Overlapping subproblems → **DP**  
- Generating all possibilities → **Recursion/Backtracking**
