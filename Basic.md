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
## string in Python
- islower()/isupper()
- upper()/lower()
- ord() 注意在Unicode表裡大寫字母們在小寫字母們的前面，而且他們之間（A和a）的差值是32
- chr()
```
char = "a"
new_char = chr(ord(char) - 32)
print(new_char)     "A"
```
- separator.join(iterable)
```
arr = ["Hello", "World"]
str = " ".join(arr)    "Hello World"
```

## Singly LinkedList Construction
需要一個class Node和class LinkedList。class Node需要有value和next，class LinkedList需要有length和head。code如下：
```
class Node:
    def __init__(self, value):
        self.value = value
        self.next = None

class LinkedList:
    def __init__(self):
        self.length = 0
        self.head = None
    
    def append(self, value):
        self.length += 1
        new_node = Node(value)

        if self.head is None:
            self.head = new_node
        else:
            current_node = self.head
            while current_node.next is not None:
                current_node = current_node.next
            current_node.next = new_node
    
    def print_ll(self):
        if self.head is None:
            return
        else:
            current_node = self.head
            while current_node is not None:
                print(current_node.value, end=" ")
                current_node = current_node.next
            return
```

## Linked List: Insert at nth + Delete at mth
這兩個都需要考慮n和m的值valid與否，然後再看n和m等於1（head node）的情況，然後再用current node和while loop的情況去寫。 
# 注意無論是刪除還是增加，current node都應該停留在n-1或者m-1
```
def insert_at_nth(self, n, value):
        if n < 1 or n > self.length + 1:
            print("Insert position out of bounds.")
            return

        new_node = Node(value)

        # 插入到头节点
        if n == 1:
            new_node.next = self.head
            self.head = new_node
        else:
            current_node = self.head
            count = 1
            while count != n - 1:
                current_node = current_node.next
                count += 1
            new_node.next = current_node.next
            current_node.next = new_node

        self.length += 1
```
```
    def delete_at_mth(self, m):
        if m < 1 or m > self.length:
            print("Delete position out of bounds.")
            return

        # 删除头节点
        if m == 1:
            self.head = self.head.next
        else:
            current_node = self.head
            count = 1
            while count != m - 1:
                current_node = current_node.next
                count += 1
            current_node.next = current_node.next.next

        self.length -= 1
```
## 
