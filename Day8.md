這是算法訓練營的第八天。開始對字符串內容的學習和應用。注意這個章節沒有基礎知識。
# 反轉字符串
這題比較簡單。就是用左右兩個指針兩兩交換。集訓營前就做過。
```
class Solution:
    def reverseString(self, s: List[str]) -> None:
        """
        Do not return anything, modify s in-place instead.
        """
        """
            First Try: Using a stack, O(n) time, O(n) space
            Second Try: Using two pointers to swap
            Third Try: Same as the second try but recursion
        """
        # left, right = 0, len(s) - 1
        # while left < right:
        #     s[left], s[right] = s[right], s[left]
        #     left += 1
        #     right -= 1

        def recursion(left, right):
            if left < right:
                s[left], s[right] = s[right], s[left]
                recursion(left+1, right-1)

        recursion(0, len(s)-1)
```
# 反轉字符串 II
```
```
# 卡碼網： 替代數字
```
```
