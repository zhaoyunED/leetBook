#RemoveLinkedListElements
Remove all elements from a linked list of integers that have value val.

Example
Given: 1 --> 2 --> 6 --> 3 --> 4 --> 5 --> 6, val = 6
Return: 1 --> 2 --> 3 --> 4 --> 5



//Ë«ÖØÖ¸Õë
ListNode* removeElements(ListNode* head, int val)
{
        ListNode** cur = &head;
        while(*cur)
        {
            ListNode* temp = *cur;
            if(temp->val == val)
            {
                *cur =(*cur)->next;
                delete temp;
            }else
                cur = &((*cur)->next);
        }
        return head;
}

//¸¨ÖúÍ·½áµã
ListNode* removeElements(ListNode* head, int val)
{
        ListNode *pseudo_head = new ListNode(0);
        pseudo_head->next = head;
        ListNode *cur = pseudo_head;
        while(cur)
        {
            if(cur->next && cur->next->val == val)
            {
                ListNode *temp = cur->next;
                cur->next = cur->next->next;
                delete temp;
            }else
                cur = cur->next;
        }
        
        return pseudo_head->next;
}
