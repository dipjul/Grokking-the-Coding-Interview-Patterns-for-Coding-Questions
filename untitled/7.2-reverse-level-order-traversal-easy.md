# 7.2 Reverse Level Order Traversal (easy)



Given the `root` of a binary tree, return _the bottom-up level order traversal of its nodes' values_. (i.e., from left to right, level by level from leaf to root).

&#x20;

**Example 1:**

![](https://assets.leetcode.com/uploads/2021/02/19/tree1.jpg)

```
Input: root = [3,9,20,null,null,15,7]
Output: [[15,7],[9,20],[3]]
```

**Example 2:**

```
Input: root = [1]
Output: [[1]]
```

**Example 3:**

```
Input: root = []
Output: []
```

```
import java.util.*;

class TreeNode {
  int val;
  TreeNode left;
  TreeNode right;

  TreeNode(int x) {
    val = x;
  }
};

class Main {
  public static List<List<Integer>> traverse(TreeNode root) {
      List<List<Integer>> result = new LinkedList<List<Integer>>();
      if(root == null) return result;
      Queue<TreeNode> queue = new LinkedList<>();
      queue.offer(root);
      
      while(!queue.isEmpty()) {
          int levelSize = queue.size();
          List<Integer> currLevel = new ArrayList<>();
          for(int i = 0; i < levelSize; i++) {
              TreeNode currNode = queue.poll();
              currLevel.add(currNode.val);
              if(currNode.left != null)
                  queue.offer(currNode.left);
              if(currNode.right != null)
                  queue.offer(currNode.right);
          }
          result.add(0,currLevel);
      }
      return result;
  }

  public static void main(String[] args) {
    TreeNode root = new TreeNode(12);
    root.left = new TreeNode(7);
    root.right = new TreeNode(1);
    root.left.left = new TreeNode(9);
    root.right.left = new TreeNode(10);
    root.right.right = new TreeNode(5);
    List<List<Integer>> result = Main.traverse(root);
    System.out.println("Reverse level order traversal: " + result);
  }
}
```

**Time complexity** [**#**](https://www.educative.io/courses/grokking-the-coding-interview/m2N6GwARL8r#time-complexity)

The time complexity of the above algorithm is O(N), where ‘N’ is the total number of nodes in the tree. This is due to the fact that we traverse each node once.

**Space complexity** [**#**](https://www.educative.io/courses/grokking-the-coding-interview/m2N6GwARL8r#space-complexity)

The space complexity of the above algorithm will be O(N) as we need to return a list containing the level order traversal. We will also need O(N) space for the queue. Since we can have a maximum of N/2 nodes at any level (this could happen only at the lowest level), therefore we will need O(N) space to store them in the queue.
