```java  
/**
 * Definition for a binary tree node.
 * public class TreeNode {
 *     int val;
 *     TreeNode left;
 *     TreeNode right;
 *     TreeNode() {}
 *     TreeNode(int val) { this.val = val; }
 *     TreeNode(int val, TreeNode left, TreeNode right) {
 *         this.val = val;
 *         this.left = left;
 *         this.right = right;
 *     }
 * }
 */
class Solution {
    public int findBottomLeftValue(TreeNode root) {
        int leftMost = 0;
        Queue<TreeNode> q = new LinkedList<>();
        q.offer(root);
        boolean firstInRow = false;
        while (!q.isEmpty()){
            int size = q.size();
            firstInRow = true;
            for (int k=0; k<size; k++) {
                TreeNode node = q.poll();
                if (firstInRow) {
                    leftMost = node.val;
                    firstInRow = false;
                }
                if (node.left != null) q.offer(node.left);
                if (node.right != null) q.offer(node.right);
            }
        }
        
        return leftMost;
    }
}
```
