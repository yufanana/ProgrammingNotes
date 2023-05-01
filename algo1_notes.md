# 02105 Algorithms and Data Structures 1

Author: __*yufanana*__ <br>
DTU Spring 2023

Compilation of key algorithms covered in the course. Includes brief description of algorithms, properties, and pseudocode.
____

### Contents<a id="top"></a>
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

## Week 1: Peaks <a id="1"></a>
[Go to top](#top)

Peak: element is at least as large as its neighbours

Peak Algorithm 1 <a id="1.1"></a>
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
```python
def peak1(A, n):
    if A[0] >= A[1]:
        return 0

    for i in range(1, n-1):
        if A[i-1] <= A[i] and A[i] >= A[i+1]:
            return i

    if A[n-2] <= A[n-1]:
        return n-1

""" 
Input (stdin)
15
1 3 7 15 17 11 2 3 6 8 7 5 9 5 23

Expected Output
4
"""

n = int(input())
A = list(map(int, input().split(" ")))

print(peak1(A, n))

```

Peak Algorithm 2 <a id="1.2"></a>
- FindMax()
- $\Theta$(n) time
```
FINDMAX(A, n)
    max = 0
    for i = 0 to n-1
        if (A[i] > A[max]) max = i
    return max
```
```python
def peak2(A, n):
    max = 0
    for i in range(n):
        if A[i] > A[max]:
            max = i
    return max
    
""" 
Input (stdin)
15
1 3 7 15 17 11 2 3 6 8 7 5 9 5 23

Expected Output
4
"""

n = int(input())
A = list(map(int, input().split(" ")))

print(peak2(A, n))

```

Peak Algorithm 3 <a id="1.3"></a>
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
```python
def peak3(A, i, j):
    m = int((i+j)/2)    # rounds down

    # bad case: m = i or j
    if m > i and A[m-1] > A[m]:
        # go left
        return peak(A, i, m-1)
    elif m < j and A[m+1] > A[m]:
        # go right
        return peak(A, m+1, j)
    else:
        return m

"""
Input (stdin)
15
1 3 7 15 17 11 2 3 6 8 7 5 9 5 23

Expected Output
9
"""

N = int(input())
A = [int(x) for x in input().split(' ')]

print(peak3(A, 0, N-1))

```

## Week 2: Search and Sort <a id="2"></a>
[Go to top](#top)

Linear Search <a id="2.1"></a>
- check if each entry matches x
- $O$(n) time

Binary search <a id="2.2"></a>
- compare x to middle entry in array
- if x is smaller, recurse on right half
- if x is larger, recurse on left half
- $O$(log n) time

```
BINARYSEARCH(A,i,j,x)
    if j < i return false
    m = ⎣(i+j)/2⎦
    if A[m] = x return true
    elseif A[m] < x return BINARYSEARCH(A,m+1,j,x)
    else return BINARYSEARCH(A,i,m-1,x) // A[m] > x
```

Insertion Sort <a id="2.3"></a>
- proceed elementwise, left to right
- insert new element into sorted subarray
- $O$(n^2) time

```
INSERTIONSORT(A, n)
    for i = 1 to n-1
        j = i
        while j > 0 and A[j-1] > A[j]
            swap A[j] and A[j-1]
            j = j - 1
```
Merge
- $O$(n) time, n=|A1|+|A2|

Merge Sort  <a id="2.4"></a>
- split array in halves
- sort each half recursively
- merge the 2 halves
- $O$(n log n) time

```
MERGESORT(A,i,j)
    if i < j
        m = ⎣ (i+j)/2 ⎦       # round down
        MERGESORT(A,i,m)
        MERGESORT(A,m+1,j)
        MERGE(A, i, m, j)
```
```python

"""
Find maximum number of rocks given a total weight.

Input (stdin)
8 15
2 5 3 1 8 4 5 7

Expected Output
5
"""
def merge_sort(A, i, j):
    if i < j:
        m = int((i+j)/2)    # round down
        merge_sort(A, i, m)
        merge_sort(A, m+1, j)
        merge(A, i, m, j)


def merge(A, i, m, j):
    l_arr = A[i:m+1]
    r_arr = A[m+1:j+1]

    p = 0   # track element in l_arr
    q = 0   # track element in r_arr
    r = i   # track element in A

    while p < len(l_arr) and q < len(r_arr):
        if l_arr[p] < r_arr[q]:
            A[r] = l_arr[p]
            p += 1
        else:
            A[r] = (r_arr[q])
            q += 1
        r += 1

    # if one side is longer than the other
    while p < len(l_arr):
        A[r] = l_arr[p]
        p += 1
        r += 1

    while q < len(r_arr):
        A[r] = r_arr[q]
        q += 1
        r += 1


def get_max_stones(N, W):
    merge_sort(N, 0, len(N)-1)
    count = 0
    total = 0
    for rock in N:
        total += rock
        if total <= W:
            count += 1
        else:
            return count
    return count

n, W = map(int, (input().split(" ")))
rocks = list(map(int, input().split(" ")))

count = get_max_stones(rocks, W)
print(count)

```

## Week 3: Analysis <a id="3"></a>
[Go to top](#top)

Running time: worst-case, best-case, average-case

Space: memory, storage, space complexity

Asymptotic Notation
- $O$: upper bound
    - f(n) = $O$(g(n)) if f(n) <= cg(n) for large n
- $\Omega$: lower bound
    - f(n) = $\Omega$(g(n)) if f(n) >= cg(n) for large n
- $\Theta$: tight bound
    - f(n) = $O$(g(n)) and f(n) = $\Omega$(g(n))

Time: exponential > polynomial > linear > log 

Experimental analysis, doubling technique: double input to measure time increase


Weekplan 3 Codejudge
```python
"""
Maximal subarray sum.

Input (stdin)
7
3 5 -9 8 2 -1 2

Output
1 11
"""
n = int(input())
numbers = list(map(int, input().split()))

best = numbers[0]   # first guess

for i in range(n):
	sum = 0
	for j in range(i, n):
		sum += numbers[j]
		if sum > best:
			best = sum

print(best)

```

## Week 4: Stacks and Queues<a id="4"></a>
[Go to top](#top)

Stack: last in first out
- push, pop, isEmpty: $\Theta$(1)
- space: $\Theta$(N)
- top variable, capacity N

```python
"""
Push, pop operations.

Input (stdin)
8
PU 3
PU 5
PU 1
PO
PU 4
PU 2
PO
PO
Expected Output
1
2
4
"""
# Read and compile inputs into a list
N = int(input())
operations = [input() for _ in range(N)]

# Initialise stack
s = [None]*N
top = -1

# Process each operation step
for step in operations:
    step = step.split(" ")
    if len(step) == 2:  # push
        element = int(step[1])
        top += 1
        s[top] = element
    else:               # pop
        if top == -1:
            print("Stack is empty")
            continue
        removed_element = s[top]
        print(removed_element)
        top -= 1

```

Queue: first in first out
- enqueue, dequeue, isEmpty: $\Theta$(1)
- space: $\Theta$(N)
- head, tail variable, capacity N

```python
"""
Enqueue, dequeue operations.

Input (stdin)
8
E 3
E 5
E 1
D
E 4
E 2
D
D
Expected Output
3
5
1
"""
# Read and compile inputs into a list
N = int(input())
operations = [input() for _ in range(N)]

# Initialise queue
q = [None]*N
head = 0
tail = 0

# Process each operation step
for step in operations:
    step = step.split(" ")
    if len(step) == 2:      # queue an element
        element = int(step[1])
        q[head] = element
        head += 1
    else:                   # dequeue
        if head == tail:
            raise Exception("Dequeue from an empty queue")
        removed_element = q[tail]
        print(removed_element)
        tail += 1

```

Linked List
- search: $\Theta$(n)
- insert, delete: $\Theta$(1)
- space: $\Theta$(N)
- head, next, prev

## Week 5: Intro to Graphs<a id="5"></a>
[Go to top](#top)

Adjacency matrix
- adjacent, insert: $O$(1)
- neighbours: $O$(n)
- space: $O$(n^2)
- `adj = [[0]*N for i in range(N)]`

Adjacency list
- adjacent, insert, neighbours: $O$(deg(v))
- space: $O$(n+m)
- `adj = [[] for i in range(n)]`

Depth-First Search <a id="5.1"></a>
- nodes: unmarked/marked
- visit all unmarked neighbours of v recursively
- until dead end, return to last position with unexplored edges
- $O$(deg(v)) on each vertex
- total time: $O$(n+m)

```python
visited = [False for i in range(n)]

def dfs(s):
    if (visited[s]):
        return
    visited[s] = True
    # print(s)
    for u in adj[s]:
        dfs(u)

dfs(0)

```

```python
'''
Check if a path exists between buildings.

Input
4 3 1 2
1 3
2 4
3 4

Expect Output
YES
'''

'''
Strategy:
- Conduct DFS or BFS from source vertex. 
- If end vertex is still unmarked after one search, it is not reachable.
- If end vertex is marked during the search, it is reachable.
'''

import sys
sys.setrecursionlimit(10000)

def reachable(adj, a, b):
    # DFS algorithm
    stack = []
    visited = [False] * n

    # Initialise
    stack.append(a)
    visited[a] = True

    # Recursive section
    while stack:                # while stack not empty
        current = stack.pop()
        for v in adj[current]:  # visit neighbors of v
            if v == b:          # found end vertex
                return True
            if not visited[v]:
                stack.append(v)
                visited[v] = True

    return False        # when stack becomes empty

# n, m, a, b = [int(i) for i in input().split()]
n, m, a , b = map(int, input().split(" "))

# use 1-indexing to mirror problem, 0th element is unused
n = n + 1

# Create graph
adj = [[] for _ in range(n)]
for _ in range(m):
    x, y = [int(i) for i in input().split()]
    adj[x].append(y)
    adj[y].append(x) # undirected graph

if reachable(adj, a, b):
    print("YES")
else:
    print("NO")

```


Breadth-First Search <a id="5.2"></a>
- nodes: unmarked/marked
- visit nodes in queue
- add neighbours to queue
- $O$(deg(v)) on each vertex
- total time: $O$(n+m)
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
Bipartite (refer to slides/notes) <a id="5.3"></a> <br>
Connectivity (refer to slides/notes)

## Week 6: Directed Graphs<a id="6"></a>
[Go to top](#top)

Adjacency matrix
- PointsTo, Insert: $O$(1)
- Neighbours: $O$(n)

Adjacency list
- PointsTo, Insert, Neighbours: $O$(deg(v))

Topological Sorting <a id="6.1"></a>
- order all vertices such that all edges are directed to the right
- find v with in-degree=0
- output v and recurse on graph with v removed
- reverse graph: $O$(n^2)
- maintain in-degree table: $O$(n+m)

```python
'''
Find minimum number of semesters needed to complete all courses given the course dependencies.

Input (stdin)
5 4
1 3
2 3
4 1
4 2
Expected Output
3
'''

# read first line of input
N, M = map(int, input().split(" "))

# use 1-indexing to mirror problem, vertex 0 unused
N = N + 1

in_deg = [0]*N
adj = [[] for _ in range(N)]

# read remaining lines of input, add edges in adj
for _ in range(M):
    x, y = [int(i) for i in input().split()]
    adj[y].append(x) # x depends on y, model as y->x, take y first before x
    in_deg[x] += 1

# in_deg==0 means course is not dependent on any other courses
current_sem = [y for y in range(1,N) if in_deg[y]==0]
sem_count = 0

while len(current_sem) != 0:
    next_sem = []
    for course in current_sem:   # for each course in the current sem
        for dep_course in adj[course]:
            in_deg[dep_course] -= 1
            if in_deg[dep_course] == 0:
                next_sem.append(dep_course)
    current_sem = next_sem
    sem_count += 1

print(sem_count)

```

Directed acyclic graph
- has topological sorting

Strongly connected components
- path from v to u, u to v

Implicit graphs <a id="6.2"></a>
- implicit representation, generated graph on-the-go

## Week 7: Priority Queues<a id="7"></a>
[Go to top](#top)

Priority Queues
- Max, ExtractMax, IncreaseKey, Insert
- Doubly-linked list: unsorted vs sorted -> different run times

Trees <a id="7.1"></a>
- graph, root node, connected, acyclic
- Depth of v: length of path from v to root
- Height of v: length of path from v to descendant leaf
- Depth of T = Height of T = length of longest path from root->leaf

Binary Tree <a id="7.2"></a>
- each node has <=2 child
- complete BT: all internal levels are full
- almost complete BT: rightmost leaves deleted
- height of almost complete BT: $\Theta$(log n)

Heap <a id="7.3"></a>
- heap-order: all keys in left and right subtree and less than v.key
- used to implement priority queue
- max heap, min heap
- Parent, Left, Right: $O$(1) time, $O$(n) space
    - Parent: return ⎣x/2⎦
    - Left: return 2x
    - Right: return 2x+1
- Building a heap
    - Top-down construction
    - Bottom-up construction
- BubbleUp, BubbleDown: $O$(log n) time
- ExtractMax, IncreaseKey, Insert: $O$(log n)
- Max: $O$(1)

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

```python
"""
Delegate tasks ID based on the task difficulty.

Input
7
N 4 5
N 9 6
N 16 3
R
N 12 8
R
R

Expected Output
9
12
4
"""

def swap(parent_idx, child_idx, heap, satellite):
    if 0 < parent_idx < child_idx < len(heap):
        if heap[parent_idx] < heap[child_idx]:
            temp = heap[parent_idx]
            heap[parent_idx] = heap[child_idx]
            heap[child_idx] = temp

            temp = satellite[parent_idx]
            satellite[parent_idx] = satellite[child_idx]
            satellite[child_idx] = temp

            return True
    return False

def bubble_up(idx, heap, satellite):
    parent_idx = idx//2
    if swap(parent_idx, idx, heap, satellite):
        bubble_up(parent_idx, heap, satellite)

def bubble_down(idx, heap, satellite):    
    # if both children exist, choose the larger one
    if len(heap) > idx*2 + 1 and heap[idx*2] < heap[idx*2 + 1]:
        child_idx = idx*2 + 1
    
    # if only the left child exists, choose that
    else:
        child_idx = idx*2

    if swap(idx, child_idx, heap, satellite):
        bubble_down(child_idx, heap, satellite)

def extract_max(heap, satellite):
    if len(heap) == 1:
        return None
    if len(heap) == 2:
        return heap.pop(), satellite.pop()
    else:
        key = heap[1]
        sat = satellite[1]
        heap[1] = heap.pop()
        satellite[1] = satellite.pop()
        bubble_down(1, heap, satellite)
        return key, sat

def insert(key, sat, heap, satellite):
    heap.append(key)
    satellite.append(sat)
    bubble_up(len(heap)-1, heap, satellite)


N = int(input())

diff_array = [None]     # heap array
id_array = [None]       # satellite array
for i in range(N):
    command = input().split(" ")    # "N id difficulty" 
    if command[0] == "N":
        key = int(command[2])
        sat = int(command[1])
        insert(key, sat, diff_array, id_array)
    else:
        diff,id_ = extract_max(diff_array, id_array)
        print(id_)

```

Heapsort <a id="7.4"></a>
- In-place sorting
- Build a heap, $O$(n) time
- n ExtractMax, $O$(n log n) time
- Total: $O$(n log n) time 

## Week 8: Union Find<a id="8"></a>
[Go to top](#top)

Union find
- Init, Union, Find

Quick Find <a id="8.1"></a>
- `id` array, where `id[i]`=representative for i
- Init, Union: $O$(n) time
- Find: read representative array, $O$(1) time
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

```python
"""
Input (stdin)
5
6
F 1
U 1 2
F 1
U 1 4
F 2
F 0
Expected Output
1
2
4
0
"""

def find(i,u):
    # Returns representative of set containing i
    return u[i]

def union(i,j,u):
    # Updates id of set i to become set j
    ri = find(i,u)  # representative of i
    rj = find(j,u)
    if ri != rj:
        for k in range(N):
            if u[k] == ri:
                u[k] = rj

# read first line of input
N = int(input())
M = int(input())

sets = list(range(0,N))
ids = sets

# Codejudge commands
for _ in range(M):
    operation = input().split(" ")
    i = int(operation[1])
    if operation[0] == 'F':     # find
        print(find(i, sets))
    if operation[0] == 'U':     # union
        j = int(operation[2])
        union(i,j,sets)

```

Quick Union <a id="8.2"></a>
- root of tree is the representative
- Find: follow path to root
- Union: make root of one tree become child of another rooti
- Init: $O$(n) time
- Union, Find: $O$(d) time

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

```python
"""
Input (stdin)
5
6
F 1
U 1 2
F 1
U 1 4
F 2
F 0
Expected Output
1
2
4
0
"""

def find(i,u):
    while i != u[i]:    # not root
        i = u[i]        # move to parent node
    return u[i]

def union(i,j,u):
    ri = find(i,u)  # representative of i
    rj = find(j,u)
    if ri != rj:
        # update root of i to become root of j
        u[ri] = rj

# Read input
N = int(input())
M = int(input())

# Initialise
u = list(range(0,N))    # each node in its own set

# Codejudge commands
for _ in range(M):
    operation = input().split(" ")
    i = int(operation[1])
    if operation[0] == 'F':     # find
        print(find(i, u))
    if operation[0] == 'U':     # union
        j = int(operation[2])
        union(i,j,u)

```

Weighted Quick Union <a id="8.3"></a>
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

```python
"""
Input (stdin)
5
6
F 1
U 1 2
F 1
U 1 4
F 2
F 0
Expected Output
1
1
1
0
"""

def find(i,u):
    # return id when current node is a root
    while i != u[i]:    # not root
        i = u[i]        # move to parent node
    return i

def union(i,j,u,sz):
    ri = find(i,u)  # representative of i
    rj = find(j,u)
    if ri != rj:    # not in the same set
        # compare sizes of subtrees using root ids
        if sz[ri] >= sz[rj]:
            # update root of j to become root of i
            u[rj] = ri
            sz[ri] += sz[rj]
        if sz[ri] < sz[rj]:
            # update root of i to become root of j
            u[ri] = rj
            sz[rj] += sz[ri]

# Read input
N = int(input())
M = int(input())

# Initialise
u = [i for i in range(N)]   # each node in its own set
sz = [1]*N

# Codejudge commands
for _ in range(M):
    operation = input().split(" ")
    i = int(operation[1])
    if operation[0] == 'F':     # find
        print(find(i, u))
    if operation[0] == 'U':     # union
        j = int(operation[2])
        union(i,j,u,sz)

```

Path Compression <a id="8.4"></a>
- Compress path on Find(), makes subsequent Find() faster
- Find, Union: $O$(n+m ackermanns(m,n))

```python
"""
Input (stdin)
5
6
F 1
U 1 2
F 1
U 1 4
F 2
F 0
Expected Output
1
1
1
0
"""

def path_compression(i,u):
    # i: root of node u
    if u[i] != i:   # not root node
        # move to parent node
        u[i] = path_compression(u[i],u)
    return u[i]

def find(i,u):
    return path_compression(i,u)

def union(i,j,u):
    ri = find(i,u)  # representative of i
    rj = find(j,u)
    if ri != rj:    # not in the same set
        # compare sizes of subtrees using root ids
        if sz[ri] >= sz[rj]:
            # update root of j to become root of i
            u[rj] = ri
            sz[ri] += sz[rj]
        if sz[ri] < sz[rj]:
            # update root of i to become root of j
            u[ri] = rj
            sz[rj] += sz[ri]

# Read input
N = int(input())
M = int(input())

# Initialise
u = [i for i in range(N)]       # list of IDs
sz = [1]*N

# Codejudge commands
for _ in range(M):
    operation = input().split(" ")
    i = int(operation[1])
    if operation[0] == 'F':     # find
        print(find(i,u))
    if operation[0] == 'U':     # union
        j = int(operation[2])
        union(i,j,u)

```

Dynamic Connectivity
- Init, Connected, Insert

```python
"""
Add computers to a computer network, check if computers are connected.

Input (stdin)
4 5
A 0 1
C 0 3
C 0 1
A 1 3
C 0 3
Expected Output
NO
YES
YES
"""

"""
Strategy:
- Implement the computer network as a dynamic family of sets.
- AddCable(A,B): any type of union (A,B)
- Connected(A,B) returns "Yes" if Find(A) == Find(B),"No" otherwise
"""

def find(i,u):
    # return id when current node is a root
    while i != u[i]:    # not root
        i = u[i]        # move to parent node
    return i


def union(i,j,u,sz):
    ri = find(i,u)  # representative of i
    rj = find(j,u)
    if ri != rj:    # not in the same set
        # compare sizes of subtrees using root ids
        if sz[ri] >= sz[rj]:
            # update root of j to become root of i
            u[rj] = ri
            sz[ri] += sz[rj]
        if sz[ri] < sz[rj]:
            # update root of i to become root of j
            u[ri] = rj
            sz[rj] += sz[ri]


# Initialise
N, M = map(int, input().split(" "))
u = [i for i in range(N)]
sz = [1 for i in range(N)]

# Codejudge commands
for i in range(M):
    cmd, i, j = input().split(" ")
    i = int(i)
    j = int(j)
    if cmd == "C":
        if find(i,u) == find(j,u):
            print("YES")
        else:
            print("NO")
    else:
        union(i,j,u,sz)
```

## Week 9: Minimum Spanning Trees<a id="9"></a>
[Go to top](#top)

- Spanning tree: T that connects all vertices, acyclic
- MST: minimum total weight
- Distinct edge weights, G is connected --> MST exists, is unique
- Cut property: For any cut, lightest cut edge is in MST
- Cycle property: For any cycle, heaviest edge is not in MST

Prim's Algorithm <a id="9.1"></a>
- Grow tree T from start vertex
- At each step, add lightest edge that is currently connected to T
- Stop when T has n-1 edges
- Total time: $O$(m log n)

Kruskal's Algorithm <a id="9.2"></a>
- Consider edges from lightest to heaviest
- At each step, add lightest edge to T if it does not create a cycle
- Stop when T has n-1 edges
- Total time: $O$(m log n)

```
KRUSKAL(G)
    Sort edges
    INIT(n)
    for all edges (u,v) i sorted order
        if (!CONNECTED(u,v))
            INSERT(u,v)
    return all inserted edges
```

```python
"""
Find the minimum cost of connecting cables between buildings, given the pairwise prices of connecting two buildings.

Input (stdin)
4 5
2 1 5
3 2 10
4 3 8
4 1 7
4 2 2
Expected Output
15
"""

# FIND and UNION are copied from QUICK-UNION
def find(i,U):
    # return id when current node is a root
    while i != U[i]:    # not root
        i = U[i]        # move to parent node
    return U[i]


def union(i,j,U,sz):
    ri = find(i,U)  # representative of i
    rj = find(j,U)
    if ri != rj:    # not in the same set
        # compare sizes of subtrees using root ids
        if sz[ri] >= sz[rj]:
            # update root of j to become root of i
            U[rj] = ri
            sz[ri] += sz[rj]
        if sz[ri] < sz[rj]:
            # update root of i to become root of j
            U[ri] = rj
            sz[rj] += sz[ri]

# Read input
N, M = map(int, input().split(" "))

# Initialise
U = list(range(N+1))        # list of IDs for each vertex
sz = [1]*(N+1)              # size of subtree containing vertex

# Codejudge commands
edges = []
for _ in range(M):
    u,v,w = map(int, input().split(" "))
    edges.append([u,v,w])

# edges = [list(map(int, input().split()) for _ in range(M))]
# length of outer list: M, length of inner list: 3
edges.sort(key= lambda x: x[2])     # sort according to weights

### Run Kruskal's Algorithm
# 1. sort edges
# 2. visited edges in order
# 3. add edge to T if not already connected

total_MST_weight = 0
edge_count = 0
for i, j, w in edges:
    if find(i,U) != find(j,U):  # not connected
        union(i,j,U,sz)         # add edge to MST using union
        total_MST_weight += w
        edge_count += 1
    if edge_count == (N-1):     # stop when MST is complete
        break

print(total_MST_weight)

```

## Week 10: Shortest Paths<a id="10"></a>
[Go to top](#top)

- Shortest paths: from start vertex to all vertices in graph
- Subpath property: any subpath of a shortest path is a shortest path

Dijkstra's Algorithm <a id="10.1"></a>
- non-negative weights
- maintain distance estimates for each vertex (length of shortest current known path)
- updates distance estimates by relaxing edges
- At each step, visit vertex with smallest distance estimate
- Relax all outgoing edges for that vertex
- once a vertex is visited, the distance estimate is final
- Total time: $O$(m log n)

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

```python
"""
Given a network of cables and signal loss through each cable, find best way to route cables with max signal quality.

Input (stdin)
3 4
1 2 6
1 3 2
3 2 3
1 3 4
Expected Output
0 5 2
"""

from heapq import heappush, heappop

# Read input
N, M = map(int, input().split(" "))

# Construct undirected graph
adj_list = [[] for I in range(N+1)]
for _ in range(M):
    u,v,w = map(int, input().split(" "))
    adj_list[u].append((v,w))
    adj_list[v].append((u,w))

source = 1

# Dijkstra's Algorithm
d = (N+1)*[None]        # dist estimates, 0-index unused
pq = [(0,source)]
# pq = [(-5, source)] # for exercise 2

while pq:
    dist, vertex = heappop(pq)
    if d[vertex] is None:   # vertex is unvisited
        d[vertex] = dist
        for u,w in adj_list[vertex]:
            heappush(pq, (dist+w,u))
            # heappush(pq, (dist + w + 5, u)) # for exercis

print(d[1:])
# print(0,*distance[2:]) # for exercise 2

```

Shortest Paths on DAGs <a id="10.2"></a>
- sort vertices in topological order
- for each vertex, relax all outgoing edges
- Total time: $O$(m+n)


## Week 11: Search Trees<a id="11"></a>
[Go to top](#top)

Dynamic Ordered Sets
- Search, Insert, Delete
- Implementation: linked lists, sorted arrays

Binary Search Trees <a id="11.1"></a>
- Search, Insert, Delete: $O$(h) time
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

Traversal <a id="11.2"></a>
- Inorder: left subtree, vertex, right subtree
- Preorder: vertex, left subtree, right subtree
- Postorder: left subtree, right subtree, vertex

Balanced Search Trees <a id="11.3"></a>
- 2-3 tree, rooted tree
- Each internal either has 2 or 3 children
    - 2-node: 1 key, 2 children
    - 3-node: 2 key, 3 children
- Symmetric order
- Perfect balance: every path from root to leaf has same length
- Height: $\Theta$(log n)
- Search, Insert, Delete: $O$(log n)

Search
- recurse in child with interval containing k
Insert
- search for x, add x at leaf
- if node > 2 keys, move middle key to parent, split children into nodes with 1 key
Delete
- search for x
- If x is a not a leaf, find node with smallest key > x.key, swap with x, and delete it.
- If too small, take from parent. Repeat if necessary.




