# Exception & Error Handling
### 🏋️ Practice — Big Exercise
---
โจทย์นี้รวมทุกเรื่องที่เรียนมา ยกเว้น Traceback  
เวลาโดยประมาณ: **20 นาที**

## โจทย์ — Student Grade System

เขียนระบบรับคะแนนนักศึกษาที่มีความสามารถดังนี้

1. รับชื่อนักศึกษาจาก input
2. รับคะแนนจาก input (ต้องเป็นตัวเลข 0-100 เท่านั้น)
3. ถ้าคะแนนไม่ใช่ตัวเลข → แจ้งเตือน
4. ถ้าคะแนนอยู่นอกช่วง 0-100 → raise ValueError พร้อมข้อความเอง
5. ถ้าสำเร็จ → แสดงชื่อและเกรด (A=90+ B=80+ C=70+ D=60+ F=ต่ำกว่า60)
6. ไม่ว่าจะเกิดอะไรขึ้น → print `"Session ended."` เสมอ

**ผลลัพธ์ที่ต้องการ**

กรณีสำเร็จ:
```
Enter student name: Alice
Enter score (0-100): 85
Alice — Grade B
Session ended.
```

กรณี input ไม่ใช่ตัวเลข:
```
Enter student name: Bob
Enter score (0-100): abc
Invalid input: score must be a number.
Session ended.
```

กรณีคะแนนนอกช่วง:
```
Enter student name: Carol
Enter score (0-100): 150
Error: Score must be between 0 and 100.
Session ended.
```

**Concepts ที่ใช้**
- `try / except`
- `multiple except`
- `else`
- `finally`
- `raise`

<details>
<summary>💡 Hint 1 — โครงสร้างที่แนะนำ</summary>

```python
def get_grade(score):
    # เขียน logic เกรดที่นี่
    pass

name = input("Enter student name: ")

try:
    # รับ score และ validate
    pass

except ValueError as e:
    # จัดการ error
    pass

else:
    # แสดงผลถ้าสำเร็จ
    pass

finally:
    # รันเสมอ
    pass
```

</details>

<details>
<summary>💡 Hint 2 — การ validate คะแนน</summary>

หลังจาก convert score เป็น int แล้ว  
ให้เช็คว่าอยู่ในช่วง 0-100 ไหม  
ถ้าไม่ → `raise ValueError("Score must be between 0 and 100.")`

</details>


```python
# เขียนโค้ดของคุณที่นี่
def get_grade(score):
    # เขียน logic เกรดที่นี่
    if 90 <= score <= 100:
        print(f"{name} - Grade A.")
    elif 80 <= score < 90:
        print(f"{name} - Grade B.")
    elif 70 <= score < 80:
        print(f"{name} - Grade C.")
    elif 60 <= score < 70:
        print(f"{name} - Grade D.")
    elif 0 <= score < 60:
        print(f"{name} - Grade F.")
    pass

name = input("Enter student name: ")

try:
    # รับ score และ validate
    score = float(input("Enter score (0 - 100): "))
    if not (0 <= score <= 100):
        raise ValueError("Error: Score must be between 0 and 100.")

except ValueError as e:
    # จัดการ error
    print("Invalid input: score must be a number.")
    pass

else:
    # แสดงผลถ้าสำเร็จ
    get_grade(score)
    pass

finally:
    # รันเสมอ
    print("Session ended.")
    pass
```

    Invalid input: score must be a number.
    Session ended.
    
