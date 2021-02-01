``` java
class Solution {
    public int maxDepth(TreeNode root) {
        return maxDepthHelper(root);
    }
    
    private int maxDepthHelper(TreeNode node) {
        if (node == null) return 0;
        
        int left = maxDepthHelper(node.left);
        int right = maxDepthHelper(node.right);
        
        return Math.max(left, right) + 1;
    }
}
```
