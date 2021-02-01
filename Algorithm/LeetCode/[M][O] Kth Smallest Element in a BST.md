#### inorder traversal
``` java
class Solution {
    int order = 0;
    int kth = 0;
    
    public int kthSmallest(TreeNode root, int k) {
        inorder(root, k);
        
        return kth;
    }
    
    private void inorder(TreeNode node, int k) {
        if (node == null) return;
        
        inorder(node.left, k);
        
        order = order + 1;
        
        if (order == k) {
            kth = node.val;
            
            return;
        }
        
        inorder(node.right, k);
    }
}
```

#### PriorityQueue
``` java
class Solution {
    public int kthSmallest(TreeNode root, int k) {
        Queue<TreeNode> queue = new LinkedList<>();
        Queue<Integer> pq = new PriorityQueue<>();
        
        queue.offer(root);
        while (! queue.isEmpty()) {
            int size = queue.size();
            
            for (int i = 0; i < size; i++) {
                TreeNode node = queue.poll();
                pq.offer(node.val);
                
                if (node.left != null) queue.offer(node.left);
                if (node.right != null) queue.offer(node.right);
            }
        }
        
        for (int count = 0; count < k - 1; count++) {
            pq.poll();
        }
        
        return pq.poll();
    }
}
```
