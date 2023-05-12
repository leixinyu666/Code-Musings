# 203.移除链表元素
虚拟头节点
ListNode* dummyhead=new ListNode(0);
dummyhead->next=head;
ListNode* cur=dummyhead;
