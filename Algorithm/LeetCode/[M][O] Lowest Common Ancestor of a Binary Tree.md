``` java
class Solution {
    class Node {
        TreeNode node;
        boolean isCommonAncestor;
        
        Node(TreeNode node, boolean isCommonAncestor) {
            this.node = node;
            this.isCommonAncestor = isCommonAncestor;
        }
    }
    
    public TreeNode lowestCommonAncestor(TreeNode root, TreeNode p, TreeNode q) {
        if (root == null || p == null || q == null) return null;
        
        Node result = helper(root, p, q);
        
        return result.node;
    }
    
    private Node helper(TreeNode node, TreeNode p, TreeNode q) {
        if (node == null) return new Node(null, false);
        
        Node left = helper(node.left, p, q);
        
        if (left.node != null && left.isCommonAncestor) return left; // 이미 LC 찾음 (왼)
        
        if (left.node != null && (node == p || node == q)) return new Node(node, true); // 이번에 LC 찾음 (왼)
        
        Node right = helper(node.right, p, q);
        
        if (right.node != null && right.isCommonAncestor) return right; // 이미 LC 찾음 (오))
        
        if (right.node != null && (node == p || node == q)) return new Node(node, true); // 이번에 LC 찾음 (오)
        
        if (left.node != null && right.node != null) return new Node(node, true); // 이번에 LC 찾음      
        
        if (left.node == null && right.node == null
           && (node == p || node == q)) return new Node(node, false); // 이번이 하나
        
        if (left.node == null && right.node == null) return new Node(null, false);
        
        if (left.node != null) return left;
        
        if (right.node != null) return right;
        
        return new Node(null, false);
    }
}
```
