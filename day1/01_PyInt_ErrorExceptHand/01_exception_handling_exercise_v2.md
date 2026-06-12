# Exception & Error Handling
### 🔧 Mini Exercise
---
แบบฝึกหัดเล็ก — ทำทีละข้อ ใช้เวลาประมาณ 5-8 นาทีต่อข้อ

## Ex 1 — try / except

โปรแกรมข้างล่างนี้รับน้ำหนัก (kg) และส่วนสูง (m) แล้วคำนวณ BMI  
แต่ถ้าผู้ใช้ใส่ข้อมูลผิด โปรแกรมจะ crash

ครอบโค้ดด้วย `try / except` ให้โปรแกรมไม่ crash  
และแสดงข้อความแจ้งเตือนแทน


```python
# BMI Calculator — ครอบด้วย try/except
try:
    weight = float(input("Enter weight (kg): "))
    height = float(input("Enter height (m): "))
    if height == 0:
        raise ValueError("Height cannot be zero.")
    bmi = weight / (height ** 2)
    print(f"Your BMI is {bmi:.2f}")
except ValueError as e:
    print(f"Error: {e}")
```

    Error: Height cannot be zero.
    

## Ex 2 — Common Exceptions

โปรแกรมข้างล่างนี้เป็นระบบ lookup ชื่อนักศึกษาจาก dict  
ครอบด้วย `try / except` ให้รับมือกับกรณีที่ key ไม่มีอยู่ใน dict


```python
# Student lookup — ครอบด้วย try/except
students = {
    "6001": "Alice",
    "6002": "Bob",
    "6003": "Carol"
}

try:
    student_id = input("Enter student ID: ")
    print("Student name:", students[student_id])
except KeyError:
    print("Error: Student not found.")
```

    Error: Student not found.
    

## Ex 3 — Multiple Except

โปรแกรมนี้รับจำนวนสินค้าและราคาต่อชิ้น แล้วคำนวณราคารวม  
โค้ดใน `try` มีให้แล้ว — เขียนเฉพาะส่วน `except` ให้ครบ

ต้องรับมือ 2 กรณี
- ผู้ใช้ใส่ข้อความแทนตัวเลข → `ValueError`
- จำนวนสินค้าเป็น 0 แล้วหาร → `ZeroDivisionError`


```python
# เขียนเฉพาะส่วน except ให้ครบ
try:
    qty   = int(input("Enter quantity: "))
    price = float(input("Enter price per item: "))
    avg   = price / qty
    print(f"Total: {qty * price:.2f} | Avg per item: {avg:.2f}")

# เขียน except ที่นี่
except ValueError:
    print("Error: Invalid input. Please enter numeric values.")
except ZeroDivisionError:
    print("Error: Quantity cannot be zero.")
```

    Error: Quantity cannot be zero.
    

## Ex 4 — else / finally

อยากได้ผลลัพธ์แบบนี้

ถ้า input เป็น `'hello'`
```
Not a valid number.
Goodbye.
```

ถ้า input เป็น `'5'`
```
5 is divisible by 7? False
Goodbye.
```

ถ้า input เป็น `'7'`
```
7 is divisible by 7? True
Goodbye.
```

<details>
<summary>💡 Hint — คลิกเพื่อดู</summary>

- โค้ดใน `try` คือ `n = int(input("Enter a number: "))`
- ใช้ `except ValueError` → print `Not a valid number.`
- ใช้ `else` → print ผลการหาร 7
- ใช้ `finally` → print `Goodbye.`

</details>


```python
# เขียนโค้ดที่นี่
try:
    a = int(input("Enter a number: "))

except ValueError:
    print("Not a valid number.")

else:
    print(f"{a} is divisible by 7?")
    if a % 7 == 0:
        print("True")    
    else:
        print("False")

finally:
    print("Goodbye.")

```

    7 is divisible by 7?
    True
    Goodbye.
    

## Ex 5 — raise

เขียนฟังก์ชัน `set_speed(speed)` ที่รับค่าความเร็ว  
ถ้าความเร็วมากกว่า 200 ให้ `raise ValueError` พร้อมข้อความของตัวเอง  
ถ้าไม่เกิน ให้ return ค่าความเร็วนั้น

แล้วเรียกใช้ฟังก์ชันด้วย try/except เพื่อจับ error


```python
# เขียน set_speed() ที่นี่
def set_speed(speed):
    if speed > 200:
        raise ValueError("Speed cannot exceed 200 km/h.")
    print(f"Speed set to {speed} km/h.")
try:
    speed = int(input("Enter speed (km/h): "))
    set_speed(speed)
except ValueError as e:
    print(f"Error: {e}")
```

    Error: Speed cannot exceed 200 km/h.
    

## Ex 6 — Reading a Traceback

รันโค้ดข้างล่างนี้ แล้วอ่าน traceback ที่ได้  
จากนั้นตอบคำถาม 4 ข้อในช่อง comment


```python
# รันโค้ดนี้ แล้วอ่าน traceback ที่ได้
def get_first(data):
    return data[0]

def process(value):
    result = get_first(value)
    return result.upper()

process([])
```


    ---------------------------------------------------------------------------

    IndexError                                Traceback (most recent call last)

    Cell In[26], line 9
          5 def process(value):
          6     result = get_first(value)
          7     return result.upper()
          8 
    ----> 9 process([])
    

    Cell In[26], line 6, in process(value)
          5 def process(value):
    ----> 6     result = get_first(value)
          7     return result.upper()
    

    Cell In[26], line 3, in get_first(data)
          2 def get_first(data):
    ----> 3     return data[0]
    

    IndexError: list index out of range



```python
# ตอบคำถามที่นี่
# 1. Error ชนิดไหนเกิดขึ้น?
#
# 2. เกิดขึ้นที่ฟังก์ชันไหน บรรทัดไหน?
#
# 3. ฟังก์ชันไหนเรียก get_first() ?
#
# 4. สาเหตุที่แท้จริงคืออะไร?
#
```

<details>
<summary>💡 เฉลย — คลิกเพื่อดู</summary>

1. `IndexError` — list index out of range
2. ฟังก์ชัน `get_first()` บรรทัด `return data[0]`
3. `process()` เป็นคนเรียก `get_first()`
4. ส่ง list ว่าง `[]` เข้าไป ทำให้ `data[0]` ไม่มี index 0

</details>
