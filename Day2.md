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

# 第二題
# 第三題
# 第四題
