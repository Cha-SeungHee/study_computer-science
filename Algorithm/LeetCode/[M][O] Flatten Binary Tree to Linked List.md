``` java
class Solution {
    TreeNode prev = null;
    
    public void flatten(TreeNode root) {
        preorder(root);
    }
    
    private void preorder(TreeNode node) {
        if (node == null) return;
        
        TreeNode left = node.left;
        TreeNode right = node.right;
        
        if (prev == null) {
            prev = node;
        } else {
            prev.left = null;
            prev.right = node;
            prev = node;
        }
        
        preorder(left);
        preorder(right);
    }
}
```
