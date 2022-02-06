# 16.2 Topological Sort (medium)

[Topological Sort](https://en.wikipedia.org/wiki/Topological\_sorting) of a directed graph (a graph with unidirectional edges) is a linear ordering of its vertices such that for every directed edge (U, V) from vertex `U` to vertex `V`, `U` comes before `V` in the ordering.

Given a directed graph, find the topological ordering of its vertices.

**Example 1:**

```
Input: Vertices=4, Edges=[3, 2], [3, 0], [2, 0], [2, 1]
Output: Following are the two valid topological sorts for the given graph:
1) 3, 2, 0, 1
2) 3, 2, 1, 0
```

![](<../.gitbook/assets/image (10).png>)

**Example 2:**

```
Input: Vertices=5, Edges=[4, 2], [4, 3], [2, 0], [2, 1], [3, 1]
Output: Following are all valid topological sorts for the given graph:
1) 4, 2, 3, 0, 1
2) 4, 3, 2, 0, 1
3) 4, 3, 2, 1, 0
4) 4, 2, 3, 1, 0
5) 4, 2, 0, 3, 1
```

**Example 3:**

```
Input:  Vertices=7, 
        Edges=[6, 4], [6, 2], [5, 3], [5, 4], [3, 0], [3, 1], [3, 2], [4, 1]
Output: Following are all valid topological sorts for the given graph:
1) 5, 6, 3, 4, 0, 1, 2
2) 6, 5, 3, 4, 0, 1, 2
3) 5, 6, 4, 3, 0, 2, 1
4) 6, 5, 4, 3, 0, 1, 2
5) 5, 6, 3, 4, 0, 2, 1
6) 5, 6, 3, 4, 1, 2, 0 
There are other valid topological ordering of the graph too.
```

**Algorithm**

1. Initialize the graph
2. Build the graph
3. Find all the sources(i.e, all the vertices with 0 in-degree
4. For each source, add it to the result and subtract one from all of its children's in-degree & if in-degree of a child become 0 add it to the source

```java
public static List<Integer> sort(int vertices, int[][] edges) {
    List<Integer> result = new ArrayList<>();
    if (vertices <= 0)
      return result;

    // 1. Initialize the graph
    HashMap<Integer, Integer> inDegree = new HashMap<>(); // count of incoming edges for every vertex
    HashMap<Integer, List<Integer>> graph = new HashMap<>(); // adjacency list graph
    for (int i = 0; i < vertices; i++) {
      inDegree.put(i, 0);
      graph.put(i, new ArrayList<Integer>());
    }

    // 2. Build the graph
    for (int i = 0; i < edges.length; i++) {
      int parent = edges[i][0], child = edges[i][1];
      // put the child into it's parent's list
      graph.get(parent).add(child);
      // increment child's inDegree
      inDegree.put(child, inDegree.get(child) + 1);
    }

    // 3. Find all sources i.e., all vertices with 0 in-degrees
    Queue<Integer> sources = new LinkedList<>();
    for (Map.Entry<Integer, Integer> entry : inDegree.entrySet()) {
      if (entry.getValue() == 0)
        sources.add(entry.getKey());
    }

    // 4. For each source, add it to the result and 
    // subtract one from all of its children's in-degrees
    // if a child's in-degree becomes zero, add it to the sources queue
    while (!sources.isEmpty()) {
      int vertex = sources.poll();
      result.add(vertex);
      // get the node's children to decrement their in-degree
      List<Integer> children = graph.get(vertex);
      for (int child : children) {
        inDegree.put(child, inDegree.get(child) - 1);
        if (inDegree.get(child) == 0)
          sources.add(child);
      }
    }
    // topological sort is not possible as the graph has a cycle
    if (result.size() != vertices)
      return new ArrayList<>();

    return result;
  }
```

**Time Complexity**&#x20;

In step ‘d’, each vertex will become a source only once and each edge will be accessed and removed once. Therefore, the time complexity of the above algorithm will be O(V+E), where ‘V’ is the total number of vertices and ‘E’ is the total number of edges in the graph.

**Space Complexity**&#x20;

The space complexity will be O(V+E), since we are storing all of the edges for each vertex in an adjacency list.
