## 打印正方形
Input一個正方形的變成，打印一個空心的正方形（只打出四個邊）
思維：正方形可以用i和j兩個index標起來，像matrix一樣；這樣我們就可以用兩個for loop來解決問題。每當i是在邊界上以及j是在邊界上時，就打*，否則打空格。注意每一行打印需要換行，別的end=“”。
  
## map() in Python
list(map(function_name, list_name))  
```
def add_five(element):
  return element + 5

list1 = [1, 2, 3, 4, 5]
list2 = list(map(add_five, list1))
```
注意map本身只返回一個iterator，需要wrap一個list來被轉換成可以print的format
  
## print() in Python
如果沒有end，默認換行；
end=“”，連續打印；
end=“ ”，空格；

## 打印n位小數
```
number = 3.1415926
# {}是一个占位符，输出结果时会将format()参数里的内容替换在{}中，:.2f 表示保留两位小数
formatted_number = "{:.2f}".format(number)
print(formatted_number)
```
