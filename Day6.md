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

# 快樂數

# 兩數之和
