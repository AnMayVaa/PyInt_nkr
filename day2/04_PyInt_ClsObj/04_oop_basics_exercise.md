# OOP — Class & Object
### 🔧 Mini Exercise
---
ทำทีละข้อ ใช้เวลาประมาณ 5-8 นาทีต่อข้อ

## Ex 1 — Class & Object

สร้าง class `Dog` ที่มีแค่ `pass` ข้างใน  
แล้วสร้าง object จากมัน 2 ตัว และ print ดูว่าได้อะไร


```python
# สร้าง class Dog และ object 2 ตัว
class Dog:
    pass

dog1 = Dog()
dog2 = Dog()
print(dog1)
print(dog2)
```

    <__main__.Dog object at 0x000001CD618256A0>
    <__main__.Dog object at 0x000001CD618C8190>
    

## Ex 2 — __init__ และ self

สร้าง class `Phone` ที่มี attributes ดังนี้
- `brand` — รับจาก parameter
- `model` — รับจาก parameter  
- `battery` — เริ่มต้นที่ 100 เสมอ ไม่ต้องรับจากข้างนอก

สร้าง object 2 เครื่อง แล้ว print ค่า attribute แต่ละตัว


```python
# สร้าง class Phone
class Phone:
    def __init__(self, brand, model, battery):
        self.brand = brand
        self.model = model
        self.battery = battery
    
phone1 = Phone("Apple", "iPhone 16", 80)
phone2 = Phone("Samsung", "Galaxy S21", 60)

print(phone1.brand, phone1.model, phone1.battery)
print(phone2.brand, phone2.model, phone2.battery)
```

    Apple iPhone 12 80
    Samsung Galaxy S21 60
    

## Ex 3 — Methods

เพิ่ม methods ให้ class `Phone` จาก Ex 2
- `make_call(self)` — print `"Calling..."` และลด battery ลง 5
- `charge(self)` — reset battery กลับเป็น 100

ลองเรียก `make_call()` 3 ครั้ง แล้ว `charge()` 1 ครั้ง  
แล้ว print battery ดูผล


```python
# เพิ่ม methods ใน Phone
class Phone:
    def __init__(self, brand, model, battery):
        self.brand = brand
        self.model = model
        self.battery = battery
    def make_call(self):
        print(f"Calling...")
        self.battery -= 5
    def charge(self):
        print(f"Charging...")
        self.battery = 100
    
    
phone1 = Phone("Apple", "iPhone 16", 80)
phone1.make_call()
phone1.make_call()
phone1.make_call()
print(phone1.battery)
phone1.charge()
print(phone1.battery)
```

    Calling...
    Calling...
    Calling...
    65
    Charging...
    100
    

## Ex 4 — __str__

เพิ่ม `__str__` ให้ class `Phone`  
เมื่อ print object ให้แสดงในรูปแบบนี้

```
Apple iPhone 15 — Battery: 100%
```


```python
# เพิ่ม __str__ ใน Phone
class Phone:
    def __init__(self, brand, model, battery):
        self.brand = brand
        self.model = model
        self.battery = battery
    def make_call(self):
        print(f"Calling...")
        self.battery -= 5
    def charge(self):
        print(f"Charging...")
        self.battery = 100
    def __str__(self):
        return f"{self.brand} {self.model} - Battery: {self.battery}%"
    
phone1 = Phone("Apple", "iPhone 15", 100)
print(phone1)
```

    Apple iPhone 15 - Battery: 100%
    
