# LeetCode Problem Solutions

## Problem 21: Merge Two Sorted Lists

**Difficulty:** Easy

**Topics:** Linked List.

**Companies:** -

### Problem Description

You are given the heads of two sorted linked lists list1 and list2.

Merge the two lists into one sorted list. The list should be made by splicing together the nodes of the first two lists.

Return the head of the merged linked list.

#### Example 1:

**Input:** `list1 = [1,2,4], list2 = [1,3,4]`

**Output:** `[1,1,2,3,4,4]`

#### Example 2:

**Input:** `list1 = [], list2 = []`

**Output:** `[]`

#### Example 3:

**Input:** `list1 = [], list2 = [0]`

**Output:** `[0]`

**Constraints:**
- The number of nodes in both lists is in the range [0, 50].
- -100 <= Node.val <= 100
- Both list1 and list2 are sorted in non-decreasing order.

### Solutions

```cpp
/**
 * Definition for singly-linked list.
 * struct ListNode {
 *     int val;
 *     ListNode *next;
 *     ListNode() : val(0), next(nullptr) {}
 *     ListNode(int x) : val(x), next(nullptr) {}
 *     ListNode(int x, ListNode *next) : val(x), next(next) {}
 * };
 */
class Solution {
public:
    ListNode* mergeTwoLists(ListNode* list1, ListNode* list2) {
        if (list1 == NULL)
            return list2;
        if (list2 == NULL)
            return list1;

        // decide which list should choose for head
        ListNode* ptr = list1;
        if (list1->val > list2->val) {
            ptr = list2;
            list2 = list2->next;
        } else {
            list1 = list1->next;
        }

        ListNode* head = ptr;

        while (list1 != NULL && list2 != NULL) {
            if (list1->val > list2->val) {
                ptr->next = list2;
                ptr = ptr->next;
                list2 = list2->next;
            } else {
                ptr->next = list1;
                ptr = ptr->next;
                list1 = list1->next;
            }
        }

        while (list1 != NULL) {
            ptr->next = list1;
            ptr = ptr->next;
            list1 = list1->next;
        }

        while (list2 != NULL) {
            ptr->next = list2;
            ptr = ptr->next;
            list2 = list2->next;
        }

        return head;
    }
};
