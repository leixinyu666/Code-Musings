# 203.移除链表元素
虚拟头节点可以省去对第一个节点的分类讨论
ListNode* dummyhead=new ListNode(0);
dummyhead->next=head;
ListNode* cur=dummyhead;
再对cur操作
# 707. 设计链表
虚拟头节点，插入，删除的步骤
# 206.反转链表
引入cur,pre,tmp，类似于交换2个元素
# 19.删除倒数第n个节点
双指针，虚拟头节点，fast先走几步，再和slow一起走，直到fast的next是空
# 142.环形链表2
## 1.判断有无环
双指针法，fast走两步，slow走一步，相遇则有环
## 2.求入口节点
分析长度关系，双指针，一个从头出发，一个从相遇点出发，两者相遇出即为入口
