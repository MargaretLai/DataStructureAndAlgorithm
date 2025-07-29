這是代碼隨想錄的第七天。繼續練習哈希法相關的內容

# 四數相加 4 Sums II
Given four integer arrays nums1, nums2, nums3, and nums4 all of length n, return the number of tuples (i, j, k, l) such that:  
- 0 <= i, j, k, l < n  
- nums1[i] + nums2[j] + nums3[k] + nums4[l] == 0

暴力想法是四重nested for loop，遍歷一次所有可能的組合，但這樣時間複雜度是n^4  
優化的算法是將四個array分成兩組，先用一個二重的nested for loop去遍歷nums1和2，存取所有元素相加的和在一個dictionary裡面，然後再用另一個二重nested for loop去在nums3和nums4用num3和4的和在dictionary裡面找target。  
### 注意dictionary的存取，key存num1+num2，value存這個和出現的次數  
```
from collections import defaultdict
class Solution:
    def fourSumCount(self, nums1: List[int], nums2: List[int], nums3: List[int], nums4: List[int]) -> int:
        d = defaultdict(int)
        
        for num1 in nums1:
            for num2 in nums2:
                d[num1+num2] += 1
        
        count = 0
        for num3 in nums3:
            for num4 in nums4:
                target_element = 0 - (num3 + num4)
                if target_element in d:
                    count += d[target_element]
        
        return count
```

# 三數之和

# 贖金信： 暫時不看。為拓展題，二刷在看。

# 四數之和

