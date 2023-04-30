# 02105 Algorithms and Data Structures 1

Author: __*yufanana*__ <br>
DTU Spring 2023

Compilation of key algorithms covered. Includes brief explanations of algorithms, properties, and pseudocode.
____

Contents
1. [Peaks](#1) <br>
    1.1 [Peak 1](#1.1) <br>
    1.2 [Peak 2](#1.2) <br>
    1.3 [Peak 3](#1.3) <br>
2. [Search and Sort](#2) <br>
    2.1 [Linear Search](#2.1) <br>
    2.2 [Binary Search](#2.2) <br>
    2.3 [Insertion Sort](#2.3) <br>
    2.4 [Merge Sort](#2.4) <br>
3. [Analysis](#3) <br>
4. [Stacks and Queues](#4) <br>
5. [Intro to Graphs](#5) <br>
    5.1 [Depth-first Search](#5.1) <br>
    5.2 [Breadth-first Search](#5.2) <br>
    5.3 [Bipartite & Connectivity](#5.3) <br>
6. [Directed Graphs](#6) <br>
    6.1 [Topological Sorting](#6.1) <br>
    6.2 [Implicit Graphs](#6.2) <br>
7. [Priority Queues](#7) <br>
    7.1 [Trees](#7.1) <br>
    7.2 [Binary Trees](#7.2) <br>
    7.3 [Heap](#7.3) <br>
    7.4 [Heap Sort](#7.4) <br>
8. [Union Find](#8) <br>
    8.1 [Quick Find](#8.1) <br>
    8.2 [Quick Union](#8.2) <br>
    8.3 [Weighted Quick Union](#8.3) <br>
    8.4 [Path Compression](#8.4) <br>
9. [Minimum Spanning Trees](#9) <br>
    9.1 [Prim's Algorithm](#9.1) <br>
    9.2 [Kruskal's Algorithm](#9.2) <br>
10. [Shortest Paths](#10) <br>
    10.1 [Dijkstra's Algorithm](#10.1) <br>
    10.2 [On DAGs](#10.2) <br>
11. [Search Trees](#11) <br>
    11.1 [Binary Search Trees](#11.1) <br>
    11.2 [Traversal](#11.2) <br>
    11.3 [Balanced Search Trees](#11.3) <br>

## Week 1: Peaks<a name="1"></a>
[Go to top](#top)

Peak: element is at least as large as its neighbours

Peak Algorithm 1<a name="1.1"></a>
- check each entry
- return first peak
- $\Theta$(n) time

```
PEAK1(A, n)
    if A[0] ≥ A[1] return 0
    for i = 1 to n-2
        if A[i-1] ≤ A[i] ≥ A[i+1] return i
    if A[n-2] ≤ A[n-1] return n-1
```

Peak Algorithm 2<a name="1.2"></a>
- FindMax()
- $\Theta$(n) time
```
FINDMAX(A, n)
    max = 0
    for i = 0 to n-1
        if (A[i] > A[max]) max = i
    return max
```

Peak Algorithm 3<a name="1.3"></a>
- consider middle entry, check neighbours
- check for peak
- search recursively in half with increasing neighbour
- $\Theta$(n) time
```
PEAK3(A,i,j)
    m = ⎣(i+j)/2)⎦
    if A[m] ≥ neighbors return m
    elseif A[m-1] > A[m]
        return PEAK3(A,i,m-1)
    elseif A[m] < A[m+1]
        return PEAK3(A,m+1,j)
```

## Week 2: Search and Sort<a name="2"></a>
[Go to top](#top)

Linear Search <a name="2.1"></a>
- check if each entry matches x
- O(n) time

Binary search <a name="2.2"></a>
- compare x to middle entry in array
- if x is smaller, recurse on right half
- if x is larger, recurse on left half
- O(log n) time

```
BINARYSEARCH(A,i,j,x)
    if j < i return false
    m = ⎣(i+j)/2⎦
    if A[m] = x return true
    elseif A[m] < x return BINARYSEARCH(A,m+1,j,x)
    else return BINARYSEARCH(A,i,m-1,x) // A[m] > x
```

Insertion Sort <a name="2.3"></a>
- proceed elementwise, left to right
- insert new element into sorted subarray
- O(n^2) time

```
INSERTIONSORT(A, n)
    for i = 1 to n-1
        j = i
        while j > 0 and A[j-1] > A[j]
            swap A[j] and A[j-1]
            j = j - 1
```
Merge
- O(n) time, n=|A1|+|A2|

Merge Sort  <a name="2.4"></a>
- split array in halves
- sort each half recursively
- merge the 2 halves
- O(n log n) time

```
MERGESORT(A,i,j)
    if i < j
        m = ⎣ (i+j)/2 ⎦       # round down
        MERGESORT(A,i,m)
        MERGESORT(A,m+1,j)
        MERGE(A, i, m, j)
```

## Week 4: Stacks and Queues<a name="4"></a>
[Go to top](#top)

Stack: last in first out
- push, pop, isEmpty: $\Theta$(1)
- space: $\Theta$(N)
- top variable, capacity N

Queue: first in first out
- enqueue, dequeue, isEmpty: $\Theta$(1)
- space: $\Theta$(N)
- head, tail variable, capacity N

Linked List
- search: $\Theta$(n)
- insert, delete: $\Theta$(1)
- space: $\Theta$(N)
- head, next, prev

## Week 5: Intro to Graphs<a name="5"></a>
[Go to top](#top)

Adjacency matrix
- adjacent, insert: O(1)
- neighbours: O(n)
- space: O(n^2)
- `adj = [[0]*N for i in range(N)]`

Adjacency list
- adjacent, insert, neighbours: O(deg(v))
- space: O(n+m)
- `adj = [[] for i in range(n)]`

Depth-First Search <a name="5.1"></a>
- nodes: unmarked/marked
- visit all unmarked neighbours of v recursively
- until dead end, return to last position with unexplored edges
- O(deg(v)) on each vertex
- total time: O(n+m)

```
visited = [False for i in range(n)]

DFS(s):
    if (visited[s]):
        return
    visited[s] = True
    # print(s)
    for u in adj[s]:
        dfs(u)

dfs(0)
```

Breadth-First Search <a name="5.2"></a>
- nodes: unmarked/marked
- visit nodes in queue
- add neighbours to queue
- O(deg(v)) on each vertex
- total time: O(n+m)
- assigns layers
- finds length of shortest path to all other vertices

```
BFS(s)
    mark s
    s.d = 0
    Q.ENQUEUE(s)
    repeat until Q.ISEMPTY()
        v = Q.DEQUEUE()
        for each unmarked neighbor u
            mark u
            u.d = v.d + 1
            u.π = v
            Q.ENQUEUE(u)
```
Bipartite (refer to slides/notes) <a name="5.3"></a> <br>
Connectivity (refer to slides/notes)

## Week 6: Directed Graphs<a name="6"></a>
[Go to top](#top)

Adjacency matrix
- PointsTo, Insert: O(1)
- Neighbours: O(n)

Adjacency list
- PointsTo, Insert, Neighbours: O(deg(v))

Topological Sorting <a name="6.1"></a>
- order all vertices such that all edges are directed to the right
- find v with in-degree=0
- output v and recurse on graph with v removed
- reverse graph: O(n^2)
- maintain in-degree table: O(n+m)

Directed acyclic graph
- has topological sorting

Strongly connected components
- path from v to u, u to v

Implicit graphs <a name="6.2"></a>
- implicit representation, generated graph on-the-go

## Week 7: Priority Queues<a name="7"></a>
[Go to top](#top)

Priority Queues
- Max, ExtractMax, IncreaseKey, Insert
- Doubly-linked list: unsorted vs sorted -> different run times

Trees <a name="7.1"></a>
- graph, root node, connected, acyclic
- Depth of v: length of path from v to root
- Height of v: length of path from v to descendant leaf
- Depth of T = Height of T = length of longest path from root->leaf

Binary Tree <a name="7.2"></a>
- each node has <=2 child
- complete BT: all internal levels are full
- almost complete BT: rightmost leaves deleted
- height of almost complete BT: $\Theta$(log n)

Heap <a name="7.3"></a>
- heap-order: all keys in left and right subtree and less than v.key
- used to implement priority queue
- max heap, min heap
- Parent, Left, Right: O(1) time, O(n) space
    - Parent: return ⎣x/2⎦
    - Left: return 2x
    - Right: return 2x+1
- Building a heap
    - Top-down construction
    - Bottom-up construction
- BubbleUp, BubbleDown: O(log n) time
- ExtractMax, IncreaseKey, Insert: O(log n)
- Max: O(1)

```
MAX()
    return H[1]

INSERT(x)
    n = n + 1
    H[n] = x
    BUBBLEUP(n)

EXTRACTMAX()
    r = H[1]
    H[1] = H[n]
    n = n - 1
    BUBBLEDOWN(1)
    return r

INCREASEKEY(x,k)
    H[x] = k
    BUBBLEUP(x)
```

Heapsort <a name="7.4"></a>
- In-place sorting
- Build a heap, O(n) time
- n ExtractMax, O(n log n) time
- Total: O(n log n) time 

## Week 8: Union Find<a name="8"></a>
[Go to top](#top)

Union find
- Init, Union, Find

Quick Find <a name="8.1"></a>
- `id` array, where `id[i]`=representative for i
- Init, Union: O(n) time
- Find: O(1) time
```
INIT(n):
    for k = 0 to n-1
        id[k] = k

FIND(i):
    return id[i]

UNION(i,j):
    iID = FIND(i)
    jID = FIND(j)
    if (iID ≠ jID)
        for k = 0 to n-1
            if (id[k] == iID)
            id[k] = jID
```

Quick Union <a name="8.2"></a>
- root of tree is the representative
- Find: follow path to root
- Union: make root of one tree become child of another rooti
- Init: O(n) time
- Union, Find: O(d) time

```
INIT(n):
    for k = 0 to n-1
        p[k] = k

FIND(i):
    while (i != p[i])
        i = p[i]
        return i

UNION(i,j):
    ri = FIND(i)
    rj = FIND(j)
    if (ri ≠ rj)
        p[ri] = rj

```

Weighted Quick Union <a name="8.3"></a>
- `sz` array, where `sz[i]`=size of subtree rooted at i
- Union: make root of smaller tree, the child of other tree
- depth of node <= log_2 n

```
UNION(i,j):
    ri = FIND(i)
    rj = FIND(j)
        if (ri ≠ rj)
            if (sz[ri] < sz[rj])
                p[ri] = rj
                sz[rj] = sz[ri] + sz[rj]
            else
                p[rj] = ri
                sz[ri] = sz[ri] + sz[rj]
```

Path Compression <a name="8.4"></a>
- Compress path on Find(), makes subsequent Find() faster
- Find, Union: O(n+m ackermanns(m,n))

Dynamic Connectivity
- Init, Connected, Insert

## Week 9: Minimum Spanning Trees<a name="9"></a>
[Go to top](#top)

- Spanning tree: T that connects all vertices, acyclic
- MST: minimum total weight
- Distinct edge weights, G is connected --> MST exists, is unique
- Cut property: For any cut, lightest cut edge is in MST
- Cycle property: For any cycle, heaviest edge is not in MST

Prim's Algorithm <a name="9.1"></a>
- Grow tree T from start vertex
- At each step, add lightest edge that is currently connected to T
- Stop when T has n-1 edges
- Total time: O(m log n)

Kruskal's Algorithm <a name="9.2"></a>
- Consider edges from lightest to heaviest
- At each step, add lightest edge to T if it does not create a cycle
- Stop when T has n-1 edges
- Total time: O(m log n)

```
KRUSKAL(G)
    Sort edges
    INIT(n)
    for all edges (u,v) i sorted order
        if (!CONNECTED(u,v))
            INSERT(u,v)
    return all inserted edges
```

## Week 10: Shortest Paths<a name="10"></a>
[Go to top](#top)

- Shortest paths: from start vertex to all vertices in graph
- Subpath property: any subpath of a shortest path is a shortest path

Dijkstra's Algorithm <a name="10.1"></a>
- non-negative weights
- maintain distance estimates for each vertex (length of shortest current known path)
- updates distance estimates by relaxing edges
- At each step, visit vertex with smallest distance estimate
- Relax all outgoing edges for that vertex
- once a vertex is visited, the distance estimate is final
- Total time: O(m log n)

```
DIJKSTRA(G, s)
    for all vertices v∈V
        v.d = ∞
        v.π = null
        INSERT(P,v)
    DECREASE-KEY(P,s,0)
    while (P ≠ ∅)
        u = EXTRACT-MIN(P)
        for all v that u point to
            RELAX(u,v)

RELAX(u,v)
    if (v.d > u.d + w(u,v))
        v.d = u.d + w(u,v)
        DECREASE-KEY(P,v,v.d)
        v.π = u
```

Shortest Paths on DAGs <a name="10.2"></a>
- sort vertices in topological order
- for each vertex, relax all outgoing edges
- Total time: O(m+n)


## Week 11: Search Trees<a name="11"></a>
[Go to top](#top)

Dynamic Ordered Sets
- Search, Insert, Delete
- Implementation: linked lists, sorted arrays

Binary Search Trees <a name="11.1"></a>
- Search, Insert, Delete: O(h) time
- symmetric order:
    - vertices in left subtree < v.key
    - vertices in right subtree > v.key

Search
- if < key, go left subtree. if > key, go right subtree.
Insert
- Search for x, add x at leaf
Delete
- 0 children: remove x
- 1 child: splice x (connect child to parent)
- 2 children: 
    - find node y with smallest key > x.key.
    - splice y and replace x with y

```
INSERT(x,v)
    if (v == null) return x
    if (x.key ≤ v.key)
        v.left = INSERT(x, v.left)
    if (x.key > v.key)
        v.right = INSERT(x, v.right)
```

Traversal <a name="11.2"></a>
- Inorder: left subtree, vertex, right subtree
- Preorder: vertex, left subtree, right subtree
- Postorder: left subtree, right subtree, vertex

Balanced Search Trees <a name="11.3"></a>
- 2-3 tree, rooted tree
- Each internal either has 2 or 3 children
    - 2-node: 1 key, 2 children
    - 3-node: 2 key, 3 children
- Symmetric order
- Perfect balance: every path from root to leaf has same length
- Height: $\Theta$(log n)
- Search, Insert, Delete: O(log n)

Search
- recurse in child with interval containing k
Insert
- search for x, add x at leaf
- if node > 2 keys, move middle key to parent, split children into nodes with 1 key
Delete
- search for x
- If x is a not a leaf, find node with smallest key > x.key, swap with x, and delete it.
- If too small, take from parent. Repeat if necessary.




