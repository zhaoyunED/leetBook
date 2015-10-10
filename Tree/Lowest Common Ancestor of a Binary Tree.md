#
Given a binary tree, find the lowest common ancestor (LCA) of two given nodes in the tree.



---




```
思路：
求两个节点的最小公共父节点有三种常用的方法

此处只列上递归的方法
TreeNode* lowestCommonAncestor(TreeNode* root, TreeNode* p, TreeNode* q)
{
        if(!root)
            return NULL;
        
        if(root == p || root == q)
            return root;
        
        TreeNode* left = lowestCommonAncestor(root->left,p,q);
        TreeNode* right = lowestCommonAncestor(root->right,p,q);
        
        if(left == NULL) return right;
        if(right==NULL) return left;
        
        return root;
}
```