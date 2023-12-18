# 24.两两交换链表中的节点
[题目跳转链接🔗](https://leetcode.cn/problems/swap-nodes-in-pairs/)
两种解法，分别是递归和迭代。比较容易想到的就是迭代，因为比较符合思考方式。LeetCode官方解法！
### 1.迭代
如果仅仅进行值交换的话，链表走到最后，但是无法进行输出。当然用一个数组存值，然后再赋值给链表也可以。为了不多此一举，可以直接进行节点的交换。
1. 首先创建一个哑节点，即ListNode dummyHead = new ListNode(0) 。然后将将哑节点的下一个指向head，即dummyHead.next = head。
2. 接着就是在循环中创建两个临时节点，分别是node1，指向temp.next，node2指向temp.next.next。（用于交换的两个节点）
3. 交换两个节点，temp -> node1 -> node2，交换之后的节点关系要变成 temp -> node2 -> node1，因此需要进行如下操作。
temp.next = node2
node1.next = node2.next
node2.next = node1
```java
class Solution {
    public ListNode swapPairs(ListNode head) {
        ListNode dummyHead = new ListNode(0);
        dummyHead.next = head;
        ListNode temp = dummyHead;
        while (temp.next != null && temp.next.next != null) {
            ListNode node1 = temp.next;
            ListNode node2 = temp.next.next;
            temp.next = node2;
            node1.next = node2.next;
            node2.next = node1;
            temp = node1;
        }
        return dummyHead.next;
    }
}
```
### 2.递归
可以通过递归的方式实现两两交换链表中的节点。
递归的终止条件是链表中没有节点，或者链表中只有一个节点，此时无法进行交换。
如果链表中至少有两个节点，则在两两交换链表中的节点之后，原始链表的头节点变成新的链表的第二个节点，原始链表的第二个节点变成新的链表的头节点。链表中的其余节点的两两交换可以递归地实现。在对链表中的其余节点递归地两两交换之后，更新节点之间的指针关系，即可完成整个链表的两两交换。
用 head 表示原始链表的头节点，新的链表的第二个节点，用 newHead 表示新的链表的头节点，原始链表的第二个节点，则原始链表中的其余节点的头节点是 newHead.next。令 head.next = swapPairs(newHead.next)，表示将其余节点进行两两交换，交换后的新的头节点为 head 的下一个节点。然后令 newHead.next = head，即完成了所有节点的交换。最后返回新的链表的头节点 newHead。
```java
class Solution {
    public ListNode swapPairs(ListNode head) {
        if (head == null || head.next == null) {
            return head;
        }
        ListNode newHead = head.next;
        head.next = swapPairs(newHead.next);
        newHead.next = head;
        return newHead;
    }
}
```
