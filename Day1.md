今天是訓練營的第一天。難度適中。耗時估計3-4小時。

## 第一題：二分法
文章連結： https://programmercarl.com/0704.%E4%BA%8C%E5%88%86%E6%9F%A5%E6%89%BE.html
影片連結：https://www.bilibili.com/video/BV1fA4y1o715?vd_source=62df5c7978d71a59d5d722c00b22afeb&spm_id_from=333.788.videopod.sections

題目是典型的二分查找法。今天學會了二分法裡面while condition以及左右指針+1，-1的處理方法。解決了二分法裡面常見由瑣碎code造成的死循環以及出錯的痛點。一共三種思路，但常用的只有兩種：左閉右閉[],左閉右開[)。

### 左閉右閉
如果採用左閉右閉的思路，while的條件是left <= right；因為當左右指針指向同一個元素時，在左閉右閉的區間裡依然成立[1,1]。如果target比中間值小，右指針移到middle - 1，因為middle已經在條件中確認過比target大了，無需再查；再加上右閉，middle - 1就包含了下一次的右邊界線。同理，當target比中間值大，左指針移到middle + 1。

### 左閉右開
如果採用左閉右開的思路，while的條件是left < right；因為在右開的情況下，兩個指針指向同一個元素無意義（數學上[1,1）不成立）。如果target比中間值小，右指針移到middle；因為右開，所以要包含middle才能確保middle - 1會在下一次循環裡面被查到。如果target比中間值大，左指針移到middle + 1；因為左閉，middle + 1就足夠包含左界線了。

### Notes
另外雖然在Python裡不需要擔心Overflow的問題。middle的取值最好還是用Java式的 middle = left + （right- left）// 2。  二分法的特點是array is in order，同時無重複元素。

## 第二題：快慢指針
文章連結： https://programmercarl.com/0027.%E7%A7%BB%E9%99%A4%E5%85%83%E7%B4%A0.html#%E6%80%9D%E8%B7%AF
影片連結： https://www.bilibili.com/video/BV12A4y1Z7LP?vd_source=62df5c7978d71a59d5d722c00b22afeb&spm_id_from=333.788.videopod.sections

題目是在一個Array裡，In-place地刪除等於target的element，並返回新的Array的長度。

### 暴力解
非常容易想到的是用Nested for loops。外面的Loop循環一次整條Array，裡面的Loop在找到要刪除的element後把後面的elements依次向前挪動一位。

### 快慢指針
運用快慢指針，就可以只用一個for loop解決兩個for loop才能解決的事情。用一個快指針走遍各個元素，尋找不等於target的元素，再用一個慢指針去存需要移動元素到位的下標。具體要多看code。

## 第三題：雙指針
文章連結：https://programmercarl.com/0977.%E6%9C%89%E5%BA%8F%E6%95%B0%E7%BB%84%E7%9A%84%E5%B9%B3%E6%96%B9.html#%E7%AE%97%E6%B3%95%E5%85%AC%E5%BC%80%E8%AF%BE 
影片連結：https://www.bilibili.com/video/BV1QB4y1D7ep?vd_source=62df5c7978d71a59d5d722c00b22afeb&spm_id_from=333.788.videopod.sections 

題目是sqrt數組中的所有元素並返回排好序的version。暴力解非常簡單，直接就**2然後sorted（）就可以。

### 雙指針（左右）
數組是排序好了的，就說明最大的sqrt值肯定在兩邊，小的肯定在中間。趨勢是從左右兩邊到中間逐漸減小。利用這個特性，可以用左右兩個指針指向數組的兩端，依次進行比較，並將較大的存到新數組裡（注意從大存到小，也就是先從新數組的右端開始存）。注意while condition是left <= right，不然會遺漏一個元素；具體也可以手動跑一個例子看到應該是小於等於，而不是只有小於。

開了個好頭。心情蠻愉悅的。希望自己好好堅持，再接再厲！