#Palindrome Linked List
Given a singly linked list, determine if it is a palindrome.

Follow up:
Could you do it in O(n) time and O(1) space?


---

思路：

是否存在O(1)空间的解法还存在争议

```
bool isPalindrome(ListNode* head) {
        if(head == NULL || head->next == NULL)
            return true;
        ListNode* slow=head;
        ListNode* fast=head;
         while(fast->next!=NULL&&fast->next->next!=NULL){
            slow=slow->next;
            fast=fast->next->next;
        }
        slow->next = reverseList(slow->next);
         slow=slow->next;
         fast = head;
        while(slow!=NULL){
            if(fast->val != slow->val)
                return false;
            slow = slow->next;
            fast = fast->next;
        }
        
        return true;
}

ListNode* reverseList(ListNode* head) {
        ListNode* pre =NULL;
        ListNode* next =NULL;
        while(head)
        {
            next = head ->next;
            head->next = pre;
            pre = head;
            head = next;
        }
        
        return pre;
}```
