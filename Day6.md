第五天休息，這是代碼隨想錄的第六天。開始對哈希表的學習和應用。

# 哈希表基礎知識
每當需要快速地查詢一個元素是否在出現集合裡，就需要考慮哈希法。本質是犧牲空間換時間。  
比如說我們需要在一間學校的數據庫裡面看一個學生是否存在，正常是O(n)，但我們也可以用一點額外空間哈希一下實現O(1)。  
我們可將學生的名字哈希化，也就是hashFunction（name），然後hash Function的本質就是將名字數據化然後取模%。再根據取模後的數值將元素存在哈希表中。  
問題是，無論哈希函數再厲害，也難免會有元素碰撞的時候Hash Collision。這時候一般有兩種方法：拉鍊法和線性探測法。拉鍊法就是以鏈表的形式將元素存起來。線性探測法就是將該元素存在index+1中。

# 有效的字母異位詞
LeetCode： #242
給兩個str分別叫s和t，看一下他們是不是anagram。代碼隨想錄上面有兩種寫法。第一種是經典哈希，使用數組作為哈希表；第二種是用defaultdict，字典。
經典哈希：
### 注意ord的運用，有時候會用到！
```
class Solution:
    def isAnagram(self, s: str, t: str) -> bool:
        record = [0] * 26

        for c in s:
            record[ord(c) - ord("a")] += 1
        for c in t:
            record[ord(c) - ord("a")] -= 1
        
        for element in record:
            if element != 0:
                return False
        return True
```

Defaultdict：
### 注意: from collections import defaultdict
```
from collections import defaultdict
class Solution:
    def isAnagram(self, s: str, t: str) -> bool:
        # Use dictionary
        s_dictionary = defaultdict(int)
        t_dictionary = defaultdict(int)

        for c in s:
            s_dictionary[c] += 1
        for c in t:
            t_dictionary[c] += 1
        
        return s_dictionary == t_dictionary
```

# 兩個數組的交集
LeetCode： #349
給兩個數組，return兩個數組的交集。注意交集裡面的元素不可以重複。題目著重介紹說return的元素不可以重複，可以是任意order，很明顯就提示用set了。Python裡面可以一行搞定：
```
    return list(set(nums1) & set(nums2))
```

或者可以用dictionary去哈希：
### 注意在找到重複元素之後，直接用del num_dict[num]來刪除字典裡面該元素的存在，避免重複添加。  
### 有空也去看看Python裡面defaul1dict的各種接口，以及和別的方法的區別。
```
from collections import defaultdict

class Solution:
    def intersection(self, nums1: List[int], nums2: List[int]) -> List[int]:
        num_dict = defaultdict(int)
        for num in nums1:
            num_dict[num] += 1
        
        result = set()
        for num in nums2:
            if num in num_dict:
                result.add(num)
                del num_dict[num]
        
        return list(result)
```
# 快樂數
LeetCode： #202
A happy number is a number defined by the following process:  

Starting with any positive integer, replace the number by the sum of the squares of its digits.  
Repeat the process until the number equals 1 (where it will stay), or it loops endlessly in a cycle which does not include 1.  
Those numbers for which this process ends in 1 are happy.  
Return true if n is a happy number, and false if not.  

Example 1:  
Input: n = 19  
Output: true  
Explanation:  
12 + 92 = 82  
82 + 22 = 68  
62 + 82 = 100  
12 + 02 + 02 = 1  

Example 2:  
Input: n = 2  
Output: false  
```
class Solution:
    def get_sum(self, n:int) -> int:
        num_str = str(n)
        result = 0
        for c in num_str:
            result += int(c) ** 2
        return result

    def isHappy(self, n: int) -> bool:
        loop = set()

        while True:
            sum = self.get_sum(n)

            if sum == 1:
                return True
            else:
                if sum in loop:
                    return False
                else:
                    loop.add(sum)
            
            n = sum
```

# 兩數之和
