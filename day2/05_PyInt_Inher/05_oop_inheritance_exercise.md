# OOP — Inheritance & Polymorphism
### 🔧 Mini Exercise
---
ทำทีละข้อ ใช้เวลาประมาณ 5-8 นาทีต่อข้อ

## Ex 1 — Inheritance (สิ่งมีชีวิต)

สร้าง class `Animal` ที่มี
- attribute: `name`, `sound`
- method: `speak(self)` — print `"<name> says <sound>"`
- `__str__` — return `"Animal: <name>"`

จากนั้นสร้าง class `Dog` และ `Cat` ที่ inherit จาก `Animal`  
โดยแต่ละตัวกำหนด sound ของตัวเองใน `__init__` ได้เลย ไม่ต้องรับจากข้างนอก

ทดสอบโดยสร้าง Dog และ Cat แล้วเรียก `speak()` และ print ทั้งสอง


```python
# สร้าง Animal, Dog, Cat
class Animal:
    def __init__(self, name, sound):
        self.name = name
        self.sound = sound

    def speak(self):
        return f"{self.name} says {self.sound}"
    
    def __str__(self):
        return f"Animal: {self.name}"
    
class Dog(Animal):
    def __init__(self, name):
        super().__init__(name, "Woof")

class Cat(Animal):
    def __init__(self, name):
        super().__init__(name, "Meow")
        
Dam = Dog("Dam")
Mew = Cat("Mew")
print(Dam.speak())
print(Mew.speak())
print(Dam)
print(Mew)
```

    Dam says Woof
    Mew says Meow
    Animal: Dam
    Animal: Mew
    

## Ex 2 — Override (หุ่นยนต์)

มี class `Animal` จาก Ex 1 อยู่แล้ว  

สร้าง class `Robot` ที่ inherit จาก `Animal` แต่มีพฤติกรรมแปลกออกไป
- `__init__` รับแค่ `name` — ไม่มี sound เพราะหุ่นยนต์ไม่มีเสียงสัตว์
- override `speak(self)` — print `"<name> says: BEEP BOOP"` แทน
- override `__str__` — return `"Robot: <name>"`
- เพิ่ม method `shutdown(self)` — print `"<name> shutting down..."` (เฉพาะ Robot)

ทดสอบโดยใส่ Dog, Cat, Robot รวมกันใน list แล้ววน loop เรียก `speak()` ทุกตัว


```python
# สร้าง Robot และทดสอบ polymorphism
class Robot(Animal):
    def __init__(self, name):
        self.name = name
        super().__init__(name, "Beep Boop")
    def __str__(self):
        return f"Robot: {self.name}"
    def shutdown(self):
        return f"{self.name} is shutting down."
    
Robo = Robot("Robo")
print(Robo.speak())
print(Robo)
```

    Robo says Beep Boop
    Robot: Robo
    
