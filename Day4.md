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
LeetCode #19
暴力解可能是就直接巡歷一次然後刪除掉。用“倒數第n個就是正數第x個的思維”去遍歷並刪除。  
實際上用到了雙指針（快慢指針），並且用的很妙：先讓fast走n+1步，在fast和slow一起走，這樣fast走到null的時候slow指向倒數第n個的前一個，剛好可以用來進行刪除的操作。  
另外，記得如果要刪第n個元素，那麼其實要到的元素是n-1個。  
```
class Solution:
    def removeNthFromEnd(self, head: Optional[ListNode], n: int) -> Optional[ListNode]:
        dummy = ListNode(0, head)
        slow, fast = dummy, dummy

        for i in range(n + 1):
            fast = fast.next

        while fast:
            fast = fast.next
            slow = slow.next
        
        slow.next = slow.next.next

        return dummy.next
```

# 此處空一題沒有視頻的，二刷回來再看

# 環型鏈表II
看一下鏈表中有沒有環，有環的話返回環開始的index。明顯雙指針（快慢指針）。  
難點是fast和slow相遇後要讓slow先回到head，然後讓兩個指針同速走，就能找到index的入口。  
## 需要注意while的condition是fast and fast.next，確保fast不會走到null，而且下一個節點不是null。
```
class Solution:
    def detectCycle(self, head: Optional[ListNode]) -> Optional[ListNode]:
        fast, slow = head, head

        while fast and fast.next:
            fast = fast.next.next
            slow = slow.next

            # If there's a cycle
            if fast == slow:
                slow = head
                while slow != fast:
                    slow = slow.next
                    fast = fast.next
                return slow
```
