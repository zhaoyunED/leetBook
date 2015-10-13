#BinaryTreePostorderTraversal
Given a binary tree, return the postorder traversal of its nodes' values.

```
For example:
Given binary tree {1,#,2,3},
   1
    \
     2
    /
   3
return [3,2,1].

```
Note: Recursive solution is trivial, could you do it iteratively?



```
题意：完成二叉树的后序遍历

方法1：迭代法

vector<int> postorderTraversal(TreeNode *root)
{
        vector<int> result;
        if(!root) return result;

        stack<TreeNode*> stack;
        stack.push(root);

        while(!stack.empty())
        {
            TreeNode* node = stack.top();
            result.push_back(node->val);
            stack.pop();

            if(node->left) stack.push(node->left);
            if(node->right) stack.push(node->right);
        }
        reverse(result.begin(), result.end());

        return result;
}

方法2：递归方法

void postorder(TreeNode *root,vector<int> &result)
{
        if(root)
        {
            postorder(root->left,result);
            postorder(root->right,result);
            result.push_back(root->val);
        }
}

vector<int> postorderTraversal(TreeNode *root)
{
        vector<int> result;
        postorder(root,result);
        return result;
}
```