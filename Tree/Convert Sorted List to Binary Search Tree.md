Given a singly linked list where elements are sorted in ascending order, convert it to a height balanced BST.





//找中间节点
TreeNode* sortedListToBST(ListNode* head)
{
         return sortedListToBST( head, NULL );
}
    
TreeNode *sortedListToBST(ListNode *head, ListNode *tail)
{
        if( head == tail )
            return NULL;
        if( head->next == tail )    // 
        {   
            TreeNode *root = new TreeNode( head->val );
            return root;
        }
        ListNode *mid = head, *temp = head;
        while( temp != tail && temp->next != tail )    // 寻找中间节点
        {
            mid = mid->next;
            temp = temp->next->next;
        }
        TreeNode *root = new TreeNode( mid->val );
        root->left = sortedListToBST( head, mid );
        root->right = sortedListToBST( mid->next, tail );
        return root;
}


//方法2  利用中序遍历的思路
//run time complexity is still O(N).
ListNode *list;
int count(ListNode *node){
        int size = 0;
        while (node) {
            ++size;
            node = node->next;
        }
        return size;
}

TreeNode *generate(int n)
{
        if (n == 0)
            return NULL;
        TreeNode *node = new TreeNode(0);
        node->left = generate(n / 2);
        node->val = list->val;
        list = list->next;
        node->right = generate(n - n / 2 - 1);
        return node;
}

TreeNode *sortedListToBST(ListNode *head)
{
        this->list = head;
        return generate(count(head));
}
