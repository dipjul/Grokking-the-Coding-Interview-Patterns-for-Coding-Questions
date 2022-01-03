# 7.7 Connect Level Order Siblings (medium)



You are given a **perfect binary tree** where all leaves are on the same level, and every parent has two children. The binary tree has the following definition:

```
struct Node {
  int val;
  Node *left;
  Node *right;
  Node *next;
}
```

Populate each next pointer to point to its next right node. If there is no next right node, the next pointer should be set to `NULL`.

Initially, all next pointers are set to `NULL`.

&#x20;

**Example 1:**

![](https://assets.leetcode.com/uploads/2019/02/14/116\_sample.png)

```
Input: root = [1,2,3,4,5,6,7]
Output: [1,#,2,3,#,4,5,6,7,#]
Explanation: Given the above perfect binary tree (Figure A), your function should populate each next pointer to point to its next right node, just like in Figure B. The serialized output is in level order as connected by the next pointers, with '#' signifying the end of each level.
```

**Example 2:**

```
Input: root = []
Output: []
```

&#x20;

**Constraints:**

* The number of nodes in the tree is in the range `[0, 212 - 1]`.
* `-1000 <= Node.val <= 1000`

```
/*
// Definition for a Node.
class Node {
    public int val;
    public Node left;
    public Node right;
    public Node next;

    public Node() {}
    
    public Node(int _val) {
        val = _val;
    }

    public Node(int _val, Node _left, Node _right, Node _next) {
        val = _val;
        left = _left;
        right = _right;
        next = _next;
    }
};
*/

class Solution {
    public Node connect(Node root) {
        // Node result = null;
        if(root == null) return null;
        Queue<Node> q = new LinkedList<>();
        q.offer(root);
        
        while(!q.isEmpty()) {
            int levelSize = q.size();
            Node prev = null;
            
            for(int i = 0; i < levelSize; i++) {
                Node curr = q.poll();
                if(prev != null)
                    prev.next = curr;
                prev = curr;
                
                if(curr.left != null) q.offer(curr.left);
                if(curr.right != null) q.offer(curr.right);
            }
        }
        return root;
    }
}
```

**Time complexity** [**#**](https://www.educative.io/courses/grokking-the-coding-interview/m2YYxXDOJ03#time-complexity)

The time complexity of the above algorithm is O(N), where ‘N’ is the total number of nodes in the tree. This is due to the fact that we traverse each node once.

**Space complexity** [**#**](https://www.educative.io/courses/grokking-the-coding-interview/m2YYxXDOJ03#space-complexity)

The space complexity of the above algorithm will be O(N), which is required for the queue. Since we can have a maximum of N/2 nodes at any level (this could happen only at the lowest level), therefore we will need O(N) space to store them in the queue.
