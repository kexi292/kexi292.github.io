-[环形链表Ⅱ](https://leetcode.cn/problems/linked-list-cycle-ii/)
问题：不太清楚其中的原理，目前的解决思路是当fast和slow相遇后，重定向slow到head。然后一起向后，再次相遇就是连接点。
-[相交链表](https://leetcode.cn/problems/intersection-of-two-linked-lists/)
问题：判断循环的条件应该是p1!=p2。因为要判断的就是把另一条链上去后（逻辑上连接，不能实际连接），相遇的就是连接点。