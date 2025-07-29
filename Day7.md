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
## 這題有難度！需要常回來看看把邏輯內化，並且徹底理解去重的部分
影片連結：https://www.bilibili.com/video/BV1GW4y127qo?vd_source=62df5c7978d71a59d5d722c00b22afeb&spm_id_from=333.788.videopod.sections 
```
class Solution:
    def threeSum(self, nums: List[int]) -> List[List[int]]:
        result = []
        nums.sort()

        for i in range(len(nums)):
            if nums[i] > 0:
                return result
            
            if i > 0 and nums[i] == nums[i - 1]:
                continue

            left = i + 1
            right = len(nums) - 1

            while right > left:
                if nums[i] + nums[left] + nums[right] == 0:
                    result.append([nums[i], nums[left], nums[right]])
                    while right > left and nums[right] == nums[right - 1]:
                        right -= 1
                    while right > left and nums[left] == nums[left + 1]:
                        left += 1
                    left += 1
                    right -= 1
                elif nums[i] + nums[left] + nums[right] < 0:
                    left += 1
                else: 
                    right -= 1

        
        return result
```
# 贖金信： 暫時不看。為拓展題，二刷在看。

# 四數之和 4 Sum I
這道題是三數之和的一個延續。在三數之和的基礎上，再在代碼最外層加一個for loop，就等於額外上一個指針。  
## 這道題和三數之和一樣有難度，需要常回來看看！
```
class Solution:
    def fourSum(self, nums: List[int], target: int) -> List[List[int]]:
        nums.sort()
        n = len(nums)
        result = []
        for i in range(n):
            if i > 0 and nums[i] == nums[i-1]:# 去重
                continue
            for j in range(i+1, n):
                if j > i+1 and nums[j] == nums[j-1]: # 去重
                    continue
                left, right = j+1, n-1
                while left < right:
                    s = nums[i] + nums[j] + nums[left] + nums[right]
                    if s == target:
                        result.append([nums[i], nums[j], nums[left], nums[right]])
                        while left < right and nums[left] == nums[left+1]:
                            left += 1
                        while left < right and nums[right] == nums[right-1]:
                            right -= 1
                        left += 1
                        right -= 1
                    elif s < target:
                        left += 1
                    else:
                        right -= 1
        return result
```
