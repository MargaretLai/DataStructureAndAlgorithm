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
给定一个字符串 s 和一个整数 k，从字符串开头算起, 每计数至 2k 个字符，就反转这 2k 个字符中的前 k 个字符。  
如果剩余字符少于 k 个，则将剩余字符全部反转。  
如果剩余字符小于 2k 但大于或等于 k 个，则反转前 k 个字符，其余字符保持原样。  
## 当需要固定规律一段一段去处理字符串的时候，要想想在for循环的表达式/while循環的遞增遞減量上做做文章。
# 這道題對邊界處理有要求！之後要回來想清楚！
### 並且swap的return要記起來，這樣返回的才是一個真正的str
```
class Solution:
    def reverseStr(self, s: str, k: int) -> str:
        i = 0
        while i < len(s):
            s = self.swap(s, i, min(i + k - 1, len(s) - 1))
            i += 2 * k
        return s
    
    def swap(self, s: str,left: int, right: int):
        s = list(s)
        while left < right:
            s[left], s[right] = s[right], s[left]

            left += 1
            right -= 1
        
        return ''.join(s)
```
# 卡碼網： 替代數字
這道題LeetCode沒有。  
给定一个字符串 s，它包含小写字母和数字字符，请编写一个函数，将字符串中的字母字符保持不变，而将每个数字字符替换为number。  
例如，对于输入字符串 "a1b2c3"，函数应该将其转换为 "anumberbnumbercnumber"。  
## 注意是用兩個指針從後面更新新數組而不是新數組，否則時間複雜度會變大。
```
class Solution(object):
    def subsitute_numbers(self, s):
        """
        :type s: str
        :rtype: str
        """
        
        count = sum(1 for char in s if char.isdigit()) # 统计数字的个数
        expand_len = len(s) + (count * 5)  # 计算扩充后字符串的大小， x->number， 每有一个数字就要增加五个长度
        res = [''] * expand_len
        
        new_index = expand_len - 1 # 指向扩充后字符串末尾
        old_index = len(s) - 1 # 指向原字符串末尾
        
        while old_index >= 0: # 从后往前， 遇到数字替换成“number”
            if s[old_index].isdigit():
                res[new_index-5:new_index+1] = "number"
                new_index -= 6
            else:
                res[new_index] = s[old_index]
                new_index -= 1
            old_index -= 1
        
        return "".join(res)
        
if __name__ == "__main__":
    solution = Solution()

    while True:
        try:
            s = input()
            result = solution.subsitute_numbers(s)
            print(result)
        except EOFError:
            break

```
