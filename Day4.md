這是算法集訓營的第四天，繼續對鏈表的練習。

# 兩輛交換鏈表節點
LeetCode #24
給一個鏈表，兩兩交換節點。注意不能夠只交換值，要真實地交換節點。  
主要還是考察鏈表的基本功，指針的操作這些。  
### 難點是要掌握循環什麼時候停止。current的作用是用來swap接下來兩個元素；利用這個作用來決定循環什麼時候停止
```
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, val=0, next=None):
#         self.val = val
#         self.next = next
class Solution:
    def swapPairs(self, head: Optional[ListNode]) -> Optional[ListNode]:
        dummy_head = ListNode()
        dummy_head.next = head
        current = dummy_head

        while current.next != None and current.next.next != None:
            temp_0 = current.next
            current.next = current.next.next
            temp_1 = current.next.next
            current.next.next = temp_0
            temp_0.next = temp_1

            current = current.next.next
        
        return dummy_head.next
```

# 刪除倒數第n個節點

