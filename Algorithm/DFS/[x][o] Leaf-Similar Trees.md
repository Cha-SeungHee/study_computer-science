```java  
class Solution {
    public boolean leafSimilar(TreeNode root1, TreeNode root2) {
        if (root1 == null && root2 == null) return false;
        if (root1 == null || root2 == null) return false;
        
        List<Integer> list1 = new ArrayList<>();
        List<Integer> list2 = new ArrayList<>();
        
        inorder(root1, list1);
        inorder(root2, list2);
        
        return isSimilar(list1, list2);
        
    }
    
    private void inorder(TreeNode node, List<Integer> list) {
        if (node == null) return;
        
        inorder(node.left, list);
        
        if (node.left == null && node.right == null) {
            list.add(node.val);
        }
        
        inorder(node.right, list);
    }
    
    private boolean isSimilar(List<Integer> list1, List<Integer> list2) {
        if (list1.size() != list2.size()) return false;
        
        boolean similar = true;
        
        for (int i=0; i<list1.size(); i++) {
            if (list1.get(i) != list2.get(i)) {
                similar = false;
                break;
            }    
        }
        
        return similar;
    }
}
```

#### 확인
1. bfs로는 왜 안되는지 고민을 했어야 했다. 충분한 고민을 하자.
