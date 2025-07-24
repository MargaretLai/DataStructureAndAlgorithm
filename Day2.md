今天是集訓營的第二天。今天狀態不怎麼樣。晚上先學一題，明天早上再起來學剩下的三題。

# 滑動窗口
題目：在一個Array裡面找一個sum大於等於target的，最短的，sub array。return 這個sub array的長度值。  
暴力解：暴力解法很容易想到，直接用Nested for loop把所有可能的sub array都遍歷一次，然後找出最短的就可以。但這個做法會超時。  

## 滑動窗口：與雙指針同理，運用兩個指針，把需要用兩個for loop的東西用一個for loop做完。只不過兩個指針的滑動始終中間保留著一些元素，像一個容器/窗口一樣，所以叫滑動窗口。

### 另外，這裡面兩個指針分別是指窗口的起始位置和結束位置。For loop裡面的下標（i）代表的是結束位置，left代表的是起始位置。
### 注意left的移動不可以用if，而是要用while，才能得出最短的sub array。

代碼：
```
        sub_length = float('inf')
        left = 0
        curr_sum = 0

        for i in range(len(nums)):
            curr_sum += nums[i]
            while curr_sum >= target:
                curr_length = i - left + 1
                sub_length = min(sub_length, curr_length)
                
                curr_sum -= nums[left]
                left += 1
        
        if sub_length != float('inf'):
            return sub_length
        else:
            return 0
```

# 螺旋矩陣
給定一個數字n，創建一個矩陣，並順時針將其填滿元素（正整數1，2，3如此類推）
這道題並沒有特別的算法，就是考察一個寫暴力解的硬能力。注意怎麼創建matrix，以及在處理邊界上堅守左閉右開或者左閉右閉原則。常回來寫寫，確保熟透。
```
class Solution:
    def generateMatrix(self, n: int) -> List[List[int]]:
        nums = [[0] * n for _ in range(n)]
        start_x, start_y = 0, 0
        mid, loop = n // 2, n // 2
        count = 1

        for offset in range(1, loop + 1):
            # Top row 
            for i in range(start_y, n - offset):
                nums[start_x][i] = count
                count += 1
            
            # Right Column
            for i in range(start_x, n - offset):
                nums[i][n - offset] = count
                count += 1

            # Bottom Row
            for i in range(n - offset, start_y, -1):
                nums[n - offset][i] = count
                count += 1
            
            # Left Column
            for i in range(n - offset, start_x, -1):
                nums[i][start_y] = count
                count += 1
            
            start_x += 1
            start_y += 1
        
        if n % 2 != 0:
            nums[mid][mid] = count
        
        return nums
```

# 第三題
# 第四題
