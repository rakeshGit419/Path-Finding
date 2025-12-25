# Path Finding

## Description
This program provides a visual demonstration of the process undergone by Dijkstra and A*


Shortest path visualizer from source point to destination point.

## Dijkstra
Dijkstra's algorithm works by first adding the starting node to a priority queue. It then takes the top node in the priority queue and looks at all of the nodes surrounding it. If the nodes are valid positions then they are added to the priority queue and the top node in the queue is deleted. These nodes that are added to the queue also have a knowledge of what node they were explored from (ie. their parent node) This process is continued until a node is discovered with the same location as the finish node. From that node, a path is created by retracing the steps to the starting node. 


# Path Finding Visualizer - Dijkstra Algorithm Explanation

This document explains how the **Dijkstra algorithm** works in the Path Finding Visualizer project, with a small grid example and step-by-step illustration.

---

## Step 0: Tiny Grid Example

We use a **3x3 grid** for simplicity:

S . .
. # .
. . F




Legend:  
- `S` = Start `(0,0)`  
- `F` = Finish `(2,2)`  
- `#` = Wall `(1,1)`  
- `.` = Empty  

---

## Step 1: Initialize

- Start node: `(0,0)` → `hops = 0`  
- Priority Queue: `[ (0,0) ]`  
- GUI: Start node green, all others white.  

---

## Step 2: Explore Neighbors of Start

Neighbors of `(0,0)`:

1. `(0,1)` → empty → mark **cyan**, `hops = 1`, last = `(0,0)`  
2. `(1,0)` → empty → mark **cyan**, `hops = 1`, last = `(0,0)`  

**Queue Update:** remove `(0,0)`, add neighbors → `[ (0,1), (1,0) ]`  
**GUI:** `(0,1)` and `(1,0)` turn cyan.

---

## Step 3: Explore Node `(0,1)`

Neighbors of `(0,1)`:

1. `(0,2)` → empty → mark cyan, `hops = 2`, last = `(0,1)`  
2. `(1,1)` → wall → ignore  
3. `(1,0)` → already visited, `hops = 1` → new hops = 2 → ignore  

**Queue Update:** `[ (1,0), (0,2) ]`  
**GUI:** `(0,2)` turns cyan.

---

## Step 4: Explore Node `(1,0)`

Neighbors:

1. `(2,0)` → empty → mark cyan, `hops = 2`, last = `(1,0)`  
2. `(1,1)` → wall → ignore  
3. `(0,1)` → already visited, hops = 1 → ignore  

**Queue Update:** `[ (0,2), (2,0) ]`  
**GUI:** `(2,0)` cyan.

---

## Step 5: Explore Node `(0,2)`

Neighbors:

1. `(1,2)` → empty → mark cyan, `hops = 3`, last = `(0,2)`  
2. `(0,1)` → already visited → ignore  

**Queue Update:** `[ (2,0), (1,2) ]`  
**GUI:** `(1,2)` cyan.

---

## Step 6: Explore Node `(2,0)`

Neighbors:

1. `(2,1)` → empty → mark cyan, `hops = 3`, last = `(2,0)`  
2. `(1,0)` → already visited → ignore  

**Queue Update:** `[ (1,2), (2,1) ]`  
**GUI:** `(2,1)` cyan.

---

## Step 7: Explore Node `(1,2)` (Finish Reached)

Neighbors:

1. `(2,2)` → finish → mark **yellow** (final path), `hops = 4`, last = `(1,2)`  
2. `(0,2)` → already visited → ignore  

- Finish reached → call `backtrack()`  
- Path reconstructed:  


(0,0) → (0,1) → (0,2) → (1,2) → (2,2)


**GUI:** Final path yellow, cyan nodes show explored area.

---

## Step 8: Key Observations

1. **Hops always increasing** → guarantees shortest path.  
2. **Node updates if shorter path found** → ensures correctness even if visited before.  
3. **Walls block exploration**, but paths around them are explored.  
4. **Visualization**:  
   - Cyan = visited/explored nodes  
   - Yellow = final shortest path  

> ✅ Dijkstra always finds the shortest path in the grid using hops and backtracking, even if the queue seems random.

---

## Summary

- Start node is added to queue.  
- Explore neighbors step by step.  
- Update hops and last visited node.  
- Backtrack from finish to start to show the final path.  
- GUI updates after each exploration for visualization.

