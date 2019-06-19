# BFS and DFS



## Breadth-first Search (BFS)

### Applications:

1. find the shortest path from the root node to the target node 
2. do traversal 

### Insight 

1. **the nodes closer to the root node will be traversed earlier**

   In the first round, we process the root node. In the second round, we process the nodes next to the root node; in the third round, we process the nodes which are two steps from the root node; so on and so forth.

   If a node `X` is added to the queue in the `kth` round, the length of the shortest path between the root node and `X` is exactly `k`. That is to say, you are already in the shortest path the first time you find the target node.

2. **The processing order of the nodes is `the exact same order` as how they were `added` to the queue, which is First-in-First-out (FIFO).**

   In each round, we process the nodes which are already in the queue one by one and add all their neighbors to the queue. It is worth noting that the newly-added nodes `will not` be traversed immediately but will be processed in the next round.

3. It will be important to determine the nodes and the edges before doing BFS in a specific question. Typically, the node will be an actual node or a status while the edge will be an actual edge or a possible transition.

### Template

1. determine the lenght of the shortest path between root and target node

## Depth-first search (DFS)

### Applications:

1. traverse/search in a tree/graph (`pre-order`, `in-order` and `post-order` traversal)

2. find the path from the root node to the target node

### Insight:

1. **we never trace back unless we reach the deepest node**

   - BFS never go deeper unless it has already visited all nodes at the current level

   - the first path you found in DFS is not always the shortest path

2. using **recursion** and **stack** 

### Template:

```Java
boolean DFS(Node cur, Node target, Set<Node> visited) {
    return true if cur is target;
    for (next : each neighbor of cur) {
        if (next is not in visited) {
            add next to visted;
            return true if DFS(next, target, visited) == true;
        }
    }
    return false;
}
```

Recursive function: using the implicit stack provided by the system, also known as the [Call Stack](https://en.wikipedia.org/wiki/Call_stack).

if the depth of recursion is too high, you will suffer from `stack overflow`

```java
/*
 * Return true if there is a path from cur to target.
 */
boolean DFS(int root, int target) {
    Set<Node> visited;
    Stack<Node> stack;
    add root to stack;
    while (s is not empty) {
        Node cur = the top element in stack;
        remove the cur from the stack;
        return true if cur is target;
        for (Node next : the neighbors of cur) {
            if (next is not in visited) {
                add next to visited;
                add next to stack;
            }
        }
    }
    return false;
}
```

The logic is exactly the same with the recursion solution. But we use `while` loop and `stack` to simulate the `system call stack` during recursion. Running through several examples manually will definitely help you understand it better.