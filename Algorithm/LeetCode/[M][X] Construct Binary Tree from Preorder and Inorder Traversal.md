``` java
class Solution {
    public TreeNode buildTree(int[] preorder, int[] inorder) {
        HashMap<Integer, Integer> map = new HashMap<>();
        
        for (int i = 0; i < inorder.length; i++) {
            map.put(inorder[i], i);
        }
        
        return buildTreeHelper(0, 0, inorder.length - 1, map, preorder, inorder);
    }
    
    private TreeNode buildTreeHelper(int preIndex, int inStart, int inEnd, HashMap<Integer, Integer> map, int[] preorder, int[] inorder) {
        if (preIndex > preorder.length || inStart > inEnd) return null;
        
        TreeNode node = new TreeNode(preorder[preIndex]);
        
        int inIndex = map.get(preorder[preIndex]);
        
        node.left = buildTreeHelper(preIndex + 1, inStart, inIndex - 1, map, preorder, inorder);
        node.right = buildTreeHelper(preIndex + inIndex - inStart + 1, inIndex + 1, inEnd, map, preorder ,inorder);
        
        return node;
    }
}
```
