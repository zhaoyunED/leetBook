#Recover Binary Search Tree
Two elements of a binary search tree (BST) are swapped by mistake.

Recover the tree without changing its structure.

Note:
A solution using O(n) space is pretty straight forward. Could you devise a constant space solution?



---


```

1. 给定一个串 {1, 4, 3, 7, 9}, 只找到 4(!<=)3, 那么只需要swap这两个节点就能recover整个树.
2. 给定一个串 {1, 9, 4, 5, 3, 10},找到 9(!<=)4 和 5(!<=)3, 
swap  9和3 可recover整个树.
我们通过两个指针one,two来记录 两个 调换的node,当发生以下情况是,就记录指针
    if(one && two)
    {
            int temp = one->val;
            one->val = two->val;
            two->val = temp;
    }
因此 one 指针 只被修改1次，two 指针 可能 被修改两次 或者1次

void recoverTree(TreeNode* root) {
        if(root ==NULL)
            return;
        TreeNode *one =NULL;
        TreeNode *two =NULL;
        TreeNode p(numeric_limits<int>::min());
        TreeNode *pre =&p;
        
        recover(root,one,two,pre);
        
        if(one && two)
        {
            int temp = one->val;
            one->val = two->val;
            two->val = temp;
        }
    }
    
    void recover(TreeNode* root,TreeNode* &one,TreeNode* &two,TreeNode* &pre)
    {
        if(root)
        {
            recover(root->left,one,two,pre);
            
            if(root->val < pre->val)
            {
                if(one ==NULL)
                    one =pre;
                two = root;
            }
            pre = root;
            recover(root->right,one,two,pre);
        }
    }
```