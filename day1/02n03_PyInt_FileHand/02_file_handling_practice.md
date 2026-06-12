# File Handling + JSON
### 🏋️ Practice — Big Exercise
---
2 โจทย์ใหญ่ — ใช้เวลาประมาณ **20 นาทีต่อข้อ**

## Practice 1 — Student Score Logger

เขียนโปรแกรมบันทึกคะแนนนักศึกษาลงไฟล์ `scores.txt`  
โดยมีความสามารถดังนี้

1. รับชื่อและคะแนนจาก input ครั้งละ 1 คน
2. บันทึกลงไฟล์ในรูปแบบ `Name: Alice | Score: 85`
3. ถามว่าจะเพิ่มคนอื่นอีกไหม ถ้าตอบ `y` → รับต่อ ถ้าตอบอื่น → หยุด
4. เมื่อหยุดแล้ว อ่านไฟล์ทั้งหมดและแสดงผล
5. รับมือกรณีคะแนนไม่ใช่ตัวเลขด้วย try/except

**ผลลัพธ์ที่ต้องการ**
```
Enter name: Alice
Enter score: 85
Add another? (y/n): y
Enter name: Bob
Enter score: abc
Invalid score — skipping Bob.
Add another? (y/n): n

--- All Scores ---
Name: Alice | Score: 85
```

**Concepts ที่ใช้:** `write`, `append`, `read`, `try/except`

<details>
<summary>💡 Hint 1 — โครงสร้างที่แนะนำ</summary>

```python
while True:
    name  = input("Enter name: ")
    score = input("Enter score: ")
    
    try:
        # validate score
        # write to file
        pass
    except ValueError:
        # skip this person
        pass
    
    again = input("Add another? (y/n): ")
    if again != "y":
        break

# read and print all
```

</details>

<details>
<summary>💡 Hint 2 — การเขียนไฟล์</summary>

ครั้งแรกใช้ `"w"` เพื่อล้างไฟล์เก่า  
ครั้งต่อไปใช้ `"a"` เพื่อต่อท้าย  

หรือจะใช้ `"a"` ตลอดก็ได้ ถ้าไม่ต้องการล้างไฟล์เก่าทุกครั้งที่รัน

</details>


```python
# เขียนโค้ดที่นี่
while True:
    name  = input("Enter name: ")
    score = input("Enter score: ")
    
    try:
        # validate score
        score = int(score)
        # write to file
        with open("scores.txt", "a") as f:
            f.write(f"{name}: | {score}\n")
        pass
    except ValueError:
        # skip this person
        print(f"Invalid score - skipping {name}")
        pass
    
    again = input("Add another? (y/n): ")
    if again != "y":
        break
    
with open("scores.txt", "r") as f:
    print("--- All Scores ---")
    print(f.read())
```

    Invalid score - skipping Bob
    --- All Scores ---
    Alice: | 85
    
    

---
## Practice 2 — JSON Contact Book

เขียนโปรแกรมสมุดผู้ติดต่อที่บันทึกข้อมูลลง `contacts.json`  
โดยมีความสามารถดังนี้

1. ถ้าไฟล์ `contacts.json` มีอยู่แล้ว → โหลดข้อมูลเดิม  
   ถ้าไม่มี → เริ่มด้วย list ว่าง
2. รับชื่อและเบอร์โทรจาก input
3. เพิ่มเข้า list แล้วบันทึกลงไฟล์ใหม่
4. แสดงรายชื่อผู้ติดต่อทั้งหมดหลังบันทึก

**ผลลัพธ์ที่ต้องการ**
```
Enter name: Alice
Enter phone: 081-234-5678

--- Contact List ---
1. Alice — 081-234-5678
```
รันครั้งที่สอง
```
Enter name: Bob
Enter phone: 089-999-0000

--- Contact List ---
1. Alice — 081-234-5678
2. Bob — 089-999-0000
```

**Concepts ที่ใช้:** `os.path.exists`, `json.load`, `json.dump`, `encoding`

<details>
<summary>💡 Hint 1 — โครงสร้างที่แนะนำ</summary>

```python
import json, os

filename = "contacts.json"

# โหลดข้อมูลเดิมถ้ามี
if os.path.exists(filename):
    # load
    pass
else:
    contacts = []

# รับข้อมูลใหม่
# เพิ่มใน list
# dump ลงไฟล์
# แสดงผล
```

</details>

<details>
<summary>💡 Hint 2 — รูปแบบข้อมูลใน list</summary>

แต่ละ contact เก็บเป็น dict เช่น

```python
{"name": "Alice", "phone": "081-234-5678"}
```

รวมอยู่ใน list

```python
[
    {"name": "Alice", "phone": "081-234-5678"},
    {"name": "Bob",   "phone": "089-999-0000"}
]
```

</details>


```python
# เขียนโค้ดที่นี่
import json, os

filename = "contacts.json"

# โหลดข้อมูลเดิมถ้ามี
if os.path.exists(filename):
    # load
    with open(filename, "r") as f:
        contacts = json.load(f)
else:
    contacts = []

# รับข้อมูลใหม่
name = str(input("Enter name: "))
phone = str(input("Enter phone: "))
# เพิ่มใน list
contacts.append({"name": name, "phone": phone})
# dump ลงไฟล์
with open(filename, "w") as f:
    json.dump(contacts, f)

# แสดงผล
print("--- All Contacts ---")
for c in contacts:
    print(f"{c['name']} - {c['phone']}")
```

    --- All Contacts ---
    Alice - 084-234-5678
    Bob - 089
     - 
    
