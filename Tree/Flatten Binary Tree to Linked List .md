#Flatten Binary Tree to Linked List
Given a binary tree, flatten it to a linked list in-place.


```
For example,
Given

         1
        / \
       2   5
      / \   \
     3   4   6
The flattened tree should look like:
   1
    \
     2
      \
       3
        \
         4
          \
           5
            \
             6

```
**Hints:
If you notice carefully in the flattened tree, each node's right child points to the next node of a pre-order traversal.**




---



```

方法1：保留prev 自底向上的生成
private TreeNode prev = null;

public void flatten(TreeNode root) {
    if (root == null)
        return;
    flatten(root.right);
    flatten(root.left);
    root.right = prev;
    root.left = null;
    prev = root;
}


方法2：
保存上一个访问的的元素lastVisited自上而下的构造

private static TreeNode lastVisited = null;

public static void flatten(TreeNode root)
{
        if(root == null)
            return;
    
        TreeNode savedRight = root.right;
        if(lastVisited != null) {
            lastVisited.left = null;
            lastVisited.right = root;
        }
        lastVisited = root;
    
        flatten(root.left);
        flatten(savedRight);
}


方法3：迭代的方法
void flatten(TreeNode *root)
{
        if(root == NULL) return;  
		while(root){  
			if(root->left){  
				TreeNode *pre = root->left;  
				while(pre->right)  
					pre = pre->right;  
				pre->right = root->right;  
				root->right = root->left;  
				root->left = NULL;  
			}  
			root = root->right;  
		}  
}

```