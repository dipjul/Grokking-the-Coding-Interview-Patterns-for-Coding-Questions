# 7.6 Level Order Successor (easy)

#### Problem Statement [#](https://www.educative.io/courses/grokking-the-coding-interview/7nO4VmA74Lr#problem-statement) <a href="#problem-statement" id="problem-statement"></a>

Given a binary tree and a node, find the level order successor of the given node in the tree. The level order successor is the node that appears right after the given node in the level order traversal.

**Example 1:**

![](<../.gitbook/assets/image (5) (1).png>)

**Example 2:**

![](<../.gitbook/assets/image (8) (1).png>)

**Example 3:**

![](<../.gitbook/assets/image (7) (1).png>)

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
  public static TreeNode findSuccessor(TreeNode root, int key) {
    TreeNode result = null;
    if(root == null) return result;
    // List<TreeNode> arr = new ArrayList<TreeNode>();
    Queue<TreeNode> queue = new LinkedList<>();
    queue.offer(root);
    while(!queue.isEmpty()) {
      int levelSize = queue.size();
      for(int i = 0; i < levelSize; i++) {
        TreeNode curr = queue.poll();
        // arr.add(curr);
        if(curr.left != null) queue.offer(curr.left);
        if(curr.right != null) queue.offer(curr.right);
        if(curr.val == key) {
          result = queue.peek();
          break;
        }
      }
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
    TreeNode result = Main.findSuccessor(root, 12);
    if (result != null)
      System.out.println(result.val + " ");
    result = Main.findSuccessor(root, 9);
    if (result != null)
      System.out.println(result.val + " ");
  }
}
```

**Time complexity** [**#**](https://www.educative.io/courses/grokking-the-coding-interview/7nO4VmA74Lr#time-complexity)

The time complexity of the above algorithm is O(N), where ‘N’ is the total number of nodes in the tree. This is due to the fact that we traverse each node once.

**Space complexity** [**#**](https://www.educative.io/courses/grokking-the-coding-interview/7nO4VmA74Lr#space-complexity)

The space complexity of the above algorithm will be O(N)which is required for the queue. Since we can have a maximum of N/2 nodes at any level (this could happen only at the lowest level), therefore we will need O(N) space to store them in the queue.
