# OOP — Class & Object
### 🏋️ Practice
---
1 โจทย์ — ใช้เวลาประมาณ **10 นาที**

## Practice — Book

สร้าง class `Book` ที่เก็บข้อมูลหนังสือ 1 เล่ม

**Attributes ที่ต้องมี**
- `title` — ชื่อหนังสือ
- `author` — ชื่อผู้แต่ง
- `pages` — จำนวนหน้า
- `is_read` — อ่านแล้วหรือยัง เริ่มต้นเป็น `False` เสมอ

**Methods ที่ต้องมี**
- `mark_as_read(self)` — เปลี่ยน `is_read` เป็น `True` และ print `"Finished: <title>"`
- `summary(self)` — print ข้อมูลหนังสือในรูปแบบนี้
```
Title  : The Hobbit
Author : J.R.R. Tolkien
Pages  : 310
Status : Read
```

**__str__**  
เมื่อ print object ให้แสดง
```
"The Hobbit" by J.R.R. Tolkien (310 pages)
```

**ทดสอบโดย**
1. สร้าง book 2 เล่ม
2. print ทั้งสองเล่ม
3. mark เล่มแรกว่าอ่านแล้ว
4. เรียก summary() ของทั้งสองเล่ม

<details>
<summary>💡 Hint — โครงสร้างที่แนะนำ</summary>

```python
class Book:
    def __init__(self, title, author, pages):
        # attributes here
        pass

    def mark_as_read(self):
        pass

    def summary(self):
        pass

    def __str__(self):
        pass
```

</details>


```python
# เขียนโค้ดที่นี่
class Book:
    def __init__(self, title, author, pages, is_read):
        self.title = title
        self.author = author
        self.pages = pages
        self.is_read = is_read
        
    def mark_as_read(self):
        self.is_read = True
        print(f"Finished: {self.title}")
        
    def summary(self):
        return f"Title  : {self.title}\nAuthor : {self.author}\nPages  : {self.pages}\nStatus : {'Read' if self.is_read else 'Not Read'}"
    
    def __str__(self):
        return f"\"{self.title}\" by {self.author} ({self.pages} pages)"

book1 = Book("The Hobbit", "J.R.R. Tolkien", 310, False)
book2 = Book("To Kill a Mockingbird", "Harper Lee", 281, False)    
print(book1)
print(book2)
book1.mark_as_read()
print(book1.summary())
print(book2.summary())
```

    "The Hobbit" by J.R.R. Tolkien (310 pages)
    "To Kill a Mockingbird" by Harper Lee (281 pages)
    Finished: The Hobbit
    Title  : The Hobbit
    Author : J.R.R. Tolkien
    Pages  : 310
    Status : Read
    Title  : To Kill a Mockingbird
    Author : Harper Lee
    Pages  : 281
    Status : Not Read
    
