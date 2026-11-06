---
aliases:
  - Floyd's Cycle
  - floyd's cycle
status: backlog
tags:
  - algo/cycle-detection
  - linked-list
  - graph
---

## 1. Summary 
- A.K.A Hare-Tortoise algorithm
- Uses two pointers, one fast and one slow, to detect cycles by detecting if both pointers ever meets. 

## 2. Mechanism
- Uses two pointers, one moving twice as fast as the other one. Then one of two things can happen:
	- Fast pointer reaches null $\rightarrow$ no cycle
	- Fast pointer eventually meets slow $\rightarrow$ cycle
- Can be adapted to find the middle (or any $N$-th from tail) element of a linked list
## 3. Implementation 
```c++
bool detectCycle(ListNode* head){
	ListNode* fast = head;
	ListNode* slow = head;
	while (fast && fast->next){
		fast = fast->next->next;
		slow = slow->next;
		if (fast == slow) return true;
	}
	return false;
}
```

