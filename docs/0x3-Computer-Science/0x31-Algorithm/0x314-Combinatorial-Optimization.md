# 0x314 Combinatorial Algorithms

- [1. Tree](#1-tree)
    - [1.1. Tree Property Problem](#11-tree-property-problem)
    - [1.2. Sequence Tree](#12-sequence-tree)
        - [1.2.1. Segment Tree](#121-segmenttree)
        - [1.2.2. Binary Index Tree:](#122-binary-index-tree)
        - [1.2.3. Radix Tree (Patricia Tree):](#123-radix-tree-patricia-tree)
    - [1.3. Binary Tree](#13-binary-tree)
        - [1.3.1. Red-Black Tree:](#131-red-black-tree)
        - [1.3.2. AVL Tree](#132-avl-tree)
    - [1.4. N-ary Tree](#14-n-ary-tree)
        - [1.4.1. B/B+ Tree](#141-bb-tree)
        - [1.4.2. BK Tree](#142-bk-tree)
- [2. Graph](#2-graph)
    - [2.1. Graph Property Problems](#21-graph-property-problems)
    - [2.2. Subgraph Problems](#22-subgraph-problems)
        - [2.2.1. Maximum Clique](#221-maximum-clique)
        - [2.2.2. MST problem (Minimum Spanning Tree)](#222-mst-problem-minimum-spanning-tree)
        - [2.2.3. SCC problem](#223-scc-problem)
    - [2.3. Edge Problems](#23-edge-problems)
        - [2.3.1. Cycle Problems](#231-cycle-problems)
        - [2.3.2. Network Flow problems](#232-network-flow-problems)
        - [2.3.3. Shortest Path](#233-shortest-path)
        - [2.3.4. Matching problems](#234-matching-problems)
        - [2.3.5. Covering problems](#235-covering-problems)
    - [2.4. Vertex Problems](#24-vertex-problems)
        - [2.4.1. Vertex Cover](#241-vertex-cover)
        - [2.4.2. Independent Set](#242-independent-set)

## 1. Tree

### 1.1. Tree Property Problem

-   **Isomorphism decision**: encoding the tree by sorting theirs children with respect to their hash
-   **centroid decomposition**: a centroid of a tree is a node which would split the tree into child trees whose number of nodes are at most half of the original tree

### 1.2. Sequence Tree

Tree structures to handle sequences.

#### 1.2.1. [Segment Tree](https://www.topcoder.com/community/competitive-programming/tutorials/binary-indexed-trees)

segment tree is good at handling range queries (e.g: RMQ)

#### 1.2.2. [Binary Index Tree](https://www.topcoder.com/community/competitive-programming/tutorials/binary-indexed-trees):

BIT (Fenwick tree) is good at handling following queries with $O(log(n))$

-   prefix sum query
-   point update query

#### 1.2.3. Radix Tree (Patricia Tree):

Trie which nodes get merged when there is only one child

-   Inverted index

### 1.3. Binary Tree

The followings are self-balancing binary search tree, the blanced tree is generally defined by
- left and right tree are recursively balanced
- left and right height has at most 1 height difference.

#### 1.3.1. [Red-Black Tree:](https://www.youtube.com/watch?v=A3JZinzkMpk)

A balanced binary tree which preserves following 4 properties.

-   each node is either red or black
-   root, leaves are black
-   red children must be black
-   black height for each node must be same

Complexity: $O(log(n))$

#### 1.3.2. AVL Tree

### 1.4. N-ary Tree

#### 1.4.1. B/B+ Tree

-   for database Indexing

#### 1.4.2. BK Tree

efficient structure for edit distance search.

## 2. Graph

Graph is defined as $G(V,E)$ where $V$ is its set of vertex and $E$ is its set of edges.

I divided graph problems into 4 types:

1.  Problems to compute general properties of a graph
2.  Problems related to subgraphs such as whether a subgraph meeting a property exist or not
3.  Problems related to edges or paths (e.g.: TSP)
4.  Problems related to vertex

### 2.1. Graph Property Problems

-   **Graph I****somorphism**: decide whether there is a bijective mapping between vertex sets of two graphs (unknown whether it is NP-complete)

### 2.2. Subgraph Problems

Bipartite graph decision

#### 2.2.1. Maximum Clique

-   NP-Complete

#### 2.2.2. MST problem (Minimum Spanning Tree)

MST problem is to compute the minimum cost subset of edges which could maintain input graph connected.

-   **Prim**: greedily connect a new vertex with minimum cost from reachable vertex set.
-   [**Kruskal**](https://github.com/xinjli/CSI/blob/master/algorithm/graph/kruskal.cpp): sort all edges based on costs and iteratively connecting new vertex

#### 2.2.3. SCC problem

Strongly Connected Component

### 2.3. Edge Problems

Problems related to paths and subsets of edges

#### 2.3.1. Cycle Problems

-   **Euler Cycle**: a cycle that visits each edge exactly once. Easy to solve by checking degree of each vertex
-   **Hamilton Cycle**: a cycle that visits each vertex exactly once. NP-hard
-   **Traveling Sales Problem (TSP)**: a cycle of least cost visiting each vertex. NP-hard

#### 2.3.2. Network Flow problems

**Max Flow**

compute max flow from one *source* to one *sink*

-   **Ford-Fulkerson**: $O(F|E|)$ basic idea is to repeat the following process: greedily find a path which can flow within remaining capacity, then increase current flow for each edge within the path and decrease the increment for the reverse edge within the path.

**Min Cut**

complement of max flow

**Multi-commodity Flow problem** [[wiki](https://en.wikipedia.org/wiki/Multi-commodity_flow_problem)]

A generalization of max flow with multiple sources and sinks

#### 2.3.3. Shortest Path

**Single Source Shortest Path**

-   **Bellman-Ford** [[C++](https://github.com/xinjli/CSI/blob/master/algorithm/graph/bellman_ford.cpp)]: Iteratively update shortest distance with all edges. It can find negative loop when the update happens more than V loops. complexity $O(|V||E|)$. used in RIP
-   **Dijsktra** [[C++](https://github.com/xinjli/CSI/blob/master/algorithm/graph/dijkstra.cpp)]: iteratively update shortest distance from shortest nodes. complexity is $O(|E|log(|V|))$ with priority queue.

**All Pairs Shortest Path**

-   **Warshall-Floyd**: for for for. complexity $O(V^3)$

#### 2.3.4. Matching problems

a matching is a subset of edges which did not share any common vertices.

$$ \mathrm{MaxMatching} + \mathrm{MinEdgeCover} = |V|$$

**Max Matching**

![](https://upload.wikimedia.org/wikipedia/commons/9/98/Maximum-matching-labels.svg)

Reference: https://upload.wikimedia.org/wikipedia/commons/9/98/Maximum-matching-labels.svg

-   NP-hard
-   bigraph max matching can be reduced to max flow problem (by adding source and sink to each side of bigraph)

**Stable Matching Problem**

-   **Gale-Shapley**: algorithm for stable matching problem. (rough idea is to propose greedily from one side until stable marriage)

#### 2.3.5. Covering problems

**Min Edge Cover**

-   NP-hard
-   complement of max matching, can also be reduced to max flow problem when it is a bigraph.

### 2.4. Vertex Problems

Min vertex cover and max independent set are complementary problems

$$\mathrm{MinVertexCover} + \mathrm{MaxIndependentSet} = |V|$$

#### 2.4.1. Vertex Cover

**Min Vertex Cover**

![](https://upload.wikimedia.org/wikipedia/commons/5/58/Vertex-cover.svg)

Reference: https://upload.wikimedia.org/wikipedia/commons/5/58/Vertex-cover.svg

-   Select a subset of vertex so that each edge is covered at by at least one vertex in the set
-   NP hard
-   the answer is same as max matching when it is a bigraph.

#### 2.4.2. Independent Set

**Min Independent Set**

-   select a subset of vertex so that none of them in subset are adjacent.
-   NP hard