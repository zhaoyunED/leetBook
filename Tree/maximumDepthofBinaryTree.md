#Maximum Depth of Binary Tree
Given a binary tree, find its maximum depth.

The maximum depth is the number of nodes along the longest path from the root node down to the farthest leaf node.

```
思路：easy级别的题目，可用DFS和BFS两种方法实现

方法1：DFS
int maxDepth(TreeNode* root)
{
        if(root)
        {
            int lmax = maxDepth(root->left);
            int rmax = maxDepth(root->right);
            return max(lmax,rmax)+1;
        }
        return 0;
}

方法2：BFS
int maxDepth(TreeNode *root)
{
    if(root == NULL)
        return 0;

    int res = 0;
    queue<TreeNode *> q;
    q.push(root);
    while(!q.empty())
    {
        ++ res;
        for(int i = 0, n = q.size(); i < n; ++ i)
        {
            TreeNode *p = q.front();
            q.pop();

            if(p -> left != NULL)
                q.push(p -> left);
            if(p -> right != NULL)
                q.push(p -> right);
        }
    }

    return res;
}
```