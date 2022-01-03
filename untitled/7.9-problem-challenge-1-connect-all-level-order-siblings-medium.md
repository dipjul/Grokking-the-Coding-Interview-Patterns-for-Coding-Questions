# 7.8 Problem Challenge 1 - Connect All Level Order Siblings (medium)

Given a binary tree, connect each node with its level order successor. The last node of each level should point to the first node of the next level.

Example 1:

![](<../.gitbook/assets/image (6).png>)

Example 2:

![](<../.gitbook/assets/image (4).png>)



```
import java.util.*;

class TreeNode {
  int val;
  TreeNode left;
  TreeNode right;
  TreeNode next;

  TreeNode(int x) {
    val = x;
    left = right = next = null;
  }
};

class Main {
  public static void connect(TreeNode root) {
    if(root == null) return;

    Queue<TreeNode> queue = new LinkedList<>();
    queue.offer(root);
    TreeNode prev = null;
    while(!queue.isEmpty()) {
      int levelSize = queue.size();
      for(int i = 0; i < levelSize; i++) {
        TreeNode curr = queue.poll();
        if(prev != null)
          prev.next = curr;
        prev = curr;

        if(curr.left != null) queue.offer(curr.left);
        if(curr.right != null) queue.offer(curr.right);
      }
    }
  }

  public static void main(String[] args) {
    TreeNode root = new TreeNode(12);
    root.left = new TreeNode(7);
    root.right = new TreeNode(1);
    root.left.left = new TreeNode(9);
    root.right.left = new TreeNode(10);
    root.right.right = new TreeNode(5);
    Main.connect(root);

    // level order traversal using 'next' pointer
    TreeNode current = root;
    System.out.println("Traversal using 'next' pointer: ");
    while (current != null) {
      System.out.print(current.val + " ");
      current = current.next;
    }
  }
}
```

**Time complexity** [**#**](https://www.educative.io/courses/grokking-the-coding-interview/m2YYxXDOJ03#time-complexity)

The time complexity of the above algorithm is O(N), where ‘N’ is the total number of nodes in the tree. This is due to the fact that we traverse each node once.

**Space complexity** [**#**](https://www.educative.io/courses/grokking-the-coding-interview/m2YYxXDOJ03#space-complexity)

The space complexity of the above algorithm will be O(N), which is required for the queue. Since we can have a maximum of N/2 nodes at any level (this could happen only at the lowest level), therefore we will need O(N) space to store them in the queue.
