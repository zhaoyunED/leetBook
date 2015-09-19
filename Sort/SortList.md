#SortList
Sort a linked list in O(n log n) time using constant space complexity.



---


//merge sortľÄŔűÓĂ

```
 思路：利用归并排序
 
 时间是O(nlgn) 但是空间的话 因为是递归会，所以为不认为这是一个O(1)空间复杂度的算法

ListNode* sortList(ListNode* head)
{
        if(head==NULL||head->next==NULL) {
            return head;
        }
    	ListNode *middle = getMiddle(head);
    	ListNode *next   = middle->next;
    	middle->next = NULL;
    	return merge(sortList(head),sortList(next));
}
    
ListNode* getMiddle(ListNode* head)
{
        ListNode* first = head;
        ListNode* second = head;
        
        while(first && second->next && second->next->next )
        {
            first = first->next;
            second = second->next->next;
        }
        
        return first;
}
    
    
ListNode* merge(ListNode* first,ListNode* second)
    {
        ListNode* dummy = new ListNode(-1);
        ListNode* curry = dummy;
        
        while(first && second)
        {
            if(first->val < second->val)
            {
                curry->next = first;
                first = first->next;
            }else{
                curry->next = second;
                second = second->next;
            }
            curry = curry->next;
        }
        
        
        if(first)
            curry->next = first;
        else
            curry->next = second;
        
        return dummy->next;
}
```