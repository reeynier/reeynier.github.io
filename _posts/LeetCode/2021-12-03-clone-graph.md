---
layout: post
title: "Clone Graph Problem"
categories: [ Algorithm, Data Structure ]
tags: [ Hash Table, Depth-First Search, Breadth-First Search, Graph ]
similar: [ Graph ]
featured: false
hidden: false
excerpt: LeetCode 133. Given a reference of a node in a connected undirected graph.

---

<br />

## Description

LeetCode Problem 133.

Given a reference of a node in a connected undirected graph.

Return a deep copy (clone) of the graph.

Each node in the graph contains a value (int) and a list (List[Node]) of its neighbors.
```
class Node {
public int val;
public List<Node> neighbors;
}
```

Test case format:

For simplicity, each node's value is the same as the node's index (1-indexed). For example, the first node with val == 1, the second node with val == 2, and so on. The graph is represented in the test case using an adjacency list.

An adjacency list is a collection of unordered lists used to represent a finite graph. Each list describes the set of neighbors of a node in the graph.

The given node will always be the first node with val = 1. You must return the copy of the given node as a reference to the cloned graph.

Example 1:
```
Input: adjList = [[2,4],[1,3],[2,4],[1,3]]
Output: [[2,4],[1,3],[2,4],[1,3]]
Explanation: There are 4 nodes in the graph.
1st node (val = 1)'s neighbors are 2nd node (val = 2) and 4th node (val = 4).
2nd node (val = 2)'s neighbors are 1st node (val = 1) and 3rd node (val = 3).
3rd node (val = 3)'s neighbors are 2nd node (val = 2) and 4th node (val = 4).
4th node (val = 4)'s neighbors are 1st node (val = 1) and 3rd node (val = 3).
```

Example 2:
```
Input: adjList = [[]]
Output: [[]]
Explanation: Note that the input contains one empty list. The graph consists of only one node with val = 1 and it does not have any neighbors.
```

Example 3:
```
Input: adjList = []
Output: []
Explanation: This an empty graph, it does not have any nodes.
```

Example 4:
```
Input: adjList = [[2],[1]]
Output: [[2],[1]]
```

Constraints:
* The number of nodes in the graph is in the range [0, 100].
* 1 <= Node.val <= 100
* Node.val is unique for each node.
* There are no repeated edges and no self-loops in the graph.
* The Graph is connected and all nodes can be visited starting from the given node.

<br />

## Sample C++ Code


```c
class Solution {
public:
    Node* cloneGraph(Node* node) {
        queue<Node*> q, qc;
        if (node == NULL)
            return NULL;
        Node* nodec = new Node(node->val);
        
        q.push(node);
        qc.push(nodec);
        
        unordered_map<Node*, Node*> cloned;
        cloned[node] = nodec;
        
        Node* n;
        Node* nc;
        while (!q.empty()) {
            n = q.front();
            q.pop();
            nc = qc.front();
            qc.pop();
            
            for (auto j : n->neighbors) {
                if (j == NULL)
                    continue;
                if (cloned.find(j) == cloned.end()) {
                    Node* jc = new Node(j->val);
                    nc->neighbors.push_back(jc);
                    q.push(j);
                    qc.push(jc);
                    cloned[j] = jc;
                } else {
                    nc->neighbors.push_back(cloned[j]);

                }
            }
        }
        
        return nodec;
    }
};
```


