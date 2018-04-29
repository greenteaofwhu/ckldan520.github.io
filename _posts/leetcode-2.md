# ***2.Add Two Numbers*** #

You are given two non-empty linked lists representing two non-negative integers. The digits are stored in reverse order and each of their nodes contain a single digit. Add the two numbers and return it as a linked list.

You may assume the two numbers do not contain any leading zero, except the number 0 itself.

Example

Input: (2 -> 4 -> 3) + (5 -> 6 -> 4)

Output: 7 -> 0 -> 8

Explanation: 342 + 465 = 807.*

思路：两个链表对应位置val值相加，如果有进位将进位标志置为1，然后进行下一个链表间操作，当有一个链表指针已经为NULL时，便使用0加上另一个链表的val值和upflag。

		/**
		 * Definition for singly-linked list.
		 * struct ListNode {
		 *     int val;
		 *     ListNode *next;
		 *     ListNode(int x) : val(x), next(NULL) {}
		 * };
		 */
		class Solution {
		public:
		    ListNode* addTwoNumbers(ListNode* l1, ListNode* l2) {
		        ListNode* pre_head = new ListNode(0);
				ListNode* head = pre_head;
				int upflag = 0;
				while(l1 || l2 || upflag)
				{
					int sum = (l1?l1->val:0) + (l2?l2->val:0)+upflag;
					upflag = sum/10;
		            head->next = new ListNode(sum%10);
		            head = head->next;
		            l1 = l1?l1->next:l1;
		            l2 = l2?l2->next:l2;
				}
				return pre_head->next;
		    }
		};