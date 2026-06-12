# File Handling + JSON
### 🔧 Mini Exercise
---
ทำทีละข้อ ใช้เวลาประมาณ 5-8 นาทีต่อข้อ  
ไฟล์ `london_bridge.txt` มีให้แล้ว — วางไว้ในโฟลเดอร์เดียวกับ notebook นี้

## Ex 1 — อ่านไฟล์ 2 แบบ

อ่านไฟล์ `london_bridge.txt` โดยเขียน **2 แบบ**
- แบบที่ 1 — เปิดและปิดไฟล์เอง (without `with`)
- แบบที่ 2 — ใช้ `with`

ทั้งสองแบบให้ print เนื้อหาออกมา


```python
# แบบที่ 1 — without with
f = open('london_bridge.txt', 'r')
data = f.read()
print(data)
f.close()
```

    London Bridge is falling down,
    Falling down, falling down,
    London Bridge is falling down,
    My fair lady.
    
    


```python
# แบบที่ 2 — with with
with open('london_bridge.txt', 'r') as f:
    data = f.read()
    print(data)
```

    London Bridge is falling down,
    Falling down, falling down,
    London Bridge is falling down,
    My fair lady.
    
    

## Ex 2 — เขียนและ append

**ขั้นที่ 1** — สร้างไฟล์ `intro.txt` แล้วเขียนแนะนำตัว 3 ประโยค 3 บรรทัด

**ขั้นที่ 2** — เพิ่มประโยคแนะนำตัวอีก 1 ประโยคต่อท้ายโดยไม่ลบของเดิม


```python
# ขั้นที่ 1 — เขียน intro.txt
with open('intro.txt', 'w') as f:
    f.write('Hello, welcome to Python programming!\n')
    f.write('This is a file handling exercise.\n')
    f.write('We will learn how to read and write files in Python.\n')
```


```python
# ขั้นที่ 2 — append ต่อท้าย
with open('intro.txt', 'a') as f:
    f.write('This is the fourth line of the file.\n')
    f.write('And this is the fifth line.\n')
```

## Ex 3 — อ่าน 3 แบบ

อ่านไฟล์ `intro.txt` ที่เพิ่งสร้าง โดยใช้ครบทั้ง 3 วิธี
- `read()`
- `readline()`
- `readlines()`

แต่ละแบบให้ print ผลลัพธ์และ `type()` ออกมาด้วย


```python
# read()
with open('intro.txt', 'r') as f:
    data = f.read()
    print(data)
```

    Hello, welcome to Python programming!
    This is a file handling exercise.
    We will learn how to read and write files in Python.
    This is the fourth line of the file.
    And this is the fifth line.
    
    


```python
# readline()
with open('intro.txt', 'r') as f:
    line1 = f.readline()
    line2 = f.readline()
    print(line1)
    print(line2)
```

    Hello, welcome to Python programming!
    
    This is a file handling exercise.
    
    


```python
# readlines()
with open('intro.txt', 'r') as f:
    lines = f.readlines()
    print(lines)
```

    ['Hello, welcome to Python programming!\n', 'This is a file handling exercise.\n', 'We will learn how to read and write files in Python.\n', 'This is the fourth line of the file.\n', 'And this is the fifth line.\n']
    

## Ex 4 — seek()

อ่านไฟล์ `intro.txt` โดย **ไม่ปิดและเปิดใหม่**

- อ่านครั้งแรกด้วย `read()` แล้วเก็บไว้ใน list
- ใช้ `seek(0)` reset cursor
- อ่านครั้งที่สองแล้ว print ออกมาเป็น string ปกติ


```python
# อ่านสองรอบโดยไม่ปิดไฟล์
with open('intro.txt', 'r') as f:
    data1 = f.read()
    print('First read:')
    print(data1)
    
    # พยายามอ่านอีกครั้งโดยไม่ปิดไฟล์
    data2 = f.read()
    print('Second read (should be empty):')
    print(data2)
    
    # ย้ายตำแหน่งอ่านกลับไปต้นไฟล์
    f.seek(0)
    data3 = f.read()
    print('Third read after seek(0):')
    print(data3)
```

    First read:
    Hello, welcome to Python programming!
    This is a file handling exercise.
    We will learn how to read and write files in Python.
    This is the fourth line of the file.
    And this is the fifth line.
    
    Second read (should be empty):
    
    Third read after seek(0):
    Hello, welcome to Python programming!
    This is a file handling exercise.
    We will learn how to read and write files in Python.
    This is the fourth line of the file.
    And this is the fifth line.
    
    

## Ex 5 — os.path.exists()

โค้ดข้างล่างนี้เปิดไฟล์โดยตรง  
เพิ่ม `os.path.exists()` เพื่อเช็คก่อนว่าไฟล์มีอยู่จริงไหม  
ถ้ามี → อ่านและ print  
ถ้าไม่มี → print แจ้งเตือน


```python
# โครงโค้ด — เพิ่ม os.path.exists() ก่อนเปิดไฟล์
import os

filename = "secret.txt"   # ไฟล์นี้ไม่มีอยู่จริง

with open(filename, "r") as f:
    print(f.read())
```


    ---------------------------------------------------------------------------

    FileNotFoundError                         Traceback (most recent call last)

    Cell In[17], line 6
          2 import os
          3 
          4 filename = "secret.txt"   # ไฟล์นี้ไม่มีอยู่จริง
          5 
    ----> 6 with open(filename, "r") as f:
          7     print(f.read())
    

    FileNotFoundError: [Errno 2] No such file or directory: 'secret.txt'


## Ex 6 — json.dump และ json.load

**ขั้นที่ 1** — เขียน dict ข้างล่างนี้ลงไฟล์ `profile.json`  
**ขั้นที่ 2** — อ่านไฟล์ `profile.json` กลับมา แล้ว print ค่าแต่ละ key ออกมา


```python
import json

profile = {
    "name": "สมชาย",
    "age": 20,
    "hobbies": ["coding", "reading", "gaming"]
}

# ขั้นที่ 1 — dump ลงไฟล์
json_filename = "profile.json"
with open(json_filename, "w") as f:
    json.dump(profile, f)
```


```python
# ขั้นที่ 2 — load กลับมาและ print แต่ละ key
with open(json_filename, "r") as f:
    loaded_profile = json.load(f)
print("Name:", loaded_profile["name"])
print("Age:", loaded_profile["age"])
print("Hobbies:", loaded_profile["hobbies"])
```

    Name: สมชาย
    Age: 20
    Hobbies: ['coding', 'reading', 'gaming']
    
