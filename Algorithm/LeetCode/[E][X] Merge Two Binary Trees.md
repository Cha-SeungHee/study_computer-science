``` java
class Solution {    
    public TreeNode mergeTrees(TreeNode t1, TreeNode t2) {        
        return mergeTreesHelper(t1, t2);
    }
    
    private TreeNode mergeTreesHelper(TreeNode t1, TreeNode t2) {
        if (t1 == null && t2 == null) return null;
        if (t1 == null) return t2;
        if (t2 == null) return t1;
        
        t1.val = t1.val + t2.val;
        
        t1.left = mergeTreesHelper(t1.left, t2.left);
        t1.right = mergeTreesHelper(t1.right, t2.right);
        
        return t1;
    }
}
```
