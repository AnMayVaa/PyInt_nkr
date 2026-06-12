# OOP — Inheritance & Polymorphism
### 🏋️ Practice
---
1 โจทย์ — ใช้เวลาประมาณ **15 นาที**

## Practice — Staff System

บริษัทมีพนักงานหลายประเภท สร้างระบบจัดการพนักงานด้วย inheritance

**class `Employee` (parent)**
- attributes: `name`, `salary`
- method `work(self)` — print `"<name> is working."`
- method `get_bonus(self)` — return `salary * 0.1`
- `__str__` — return `"<name> | Salary: <salary>"`

**class `Manager` (child)**
- เพิ่ม attribute `team_size` — จำนวนคนในทีม
- override `work(self)` — print `"<name> is managing a team of <team_size>."`
- override `get_bonus(self)` — Manager ได้ bonus มากกว่า คือ `salary * 0.2`
- override `__str__` — return `"<name> | Salary: <salary> | Team: <team_size>"`

**ทดสอบโดย**
1. สร้าง Employee 2 คน Manager 1 คน
2. ใส่ทั้งหมดใน list แล้ววน loop
3. ใน loop ให้เรียก `work()`, print bonus, และ print object

**ผลลัพธ์ที่ต้องการ**
```
Alice is working.
Bonus: 3000.0
Alice | Salary: 30000

Bob is working.
Bonus: 2500.0
Bob | Salary: 25000

Carol is managing a team of 5.
Bonus: 10000.0
Carol | Salary: 50000 | Team: 5
```

<details>
<summary>💡 Hint — โครงสร้างที่แนะนำ</summary>

```python
class Employee:
    def __init__(self, name, salary):
        pass

    def work(self):
        pass

    def get_bonus(self):
        pass

    def __str__(self):
        pass


class Manager(Employee):
    def __init__(self, name, salary, team_size):
        super().__init__(name, salary)
        # add team_size here
        pass

    # override work, get_bonus, __str__
```

</details>


```python
# เขียนโค้ดที่นี่
class Employee:
    def __init__(self, name, salary):
        self.name = name
        self.salary = salary

    def work(self):
        print(f"{self.name} is working.")

    def get_bonus(self):
        return self.salary * 0.1

    def __str__(self):
        return f"{self.name} | Salary: {self.salary}"


class Manager(Employee):
    def __init__(self, name, salary, team_size):
        super().__init__(name, salary)
        self.team_size = team_size

    def work(self):
        print(f"{self.name} is managing a team of {self.team_size} people.")

    def get_bonus(self):
        return self.salary * 0.2

    def __str__(self):
        return f"{self.name} | Salary: {self.salary} | Team Size: {self.team_size}"
    
# สร้าง object ของ Employee และ Manager
employee1 = Employee("Alice", 30000)
employee2 = Employee("Bob", 25000)
manager1 = Manager("Carol", 50000, 5)

# แสดงข้อมูลและโบนัสของแต่ละ object
employees = [employee1, employee2, manager1]
for emp in employees:
    emp.work()
    print(f"Bonus: {emp.get_bonus()}")
    print(f"{emp}\n")
```

    Alice is working.
    Bonus: 3000.0
    Alice | Salary: 30000
    
    Bob is working.
    Bonus: 2500.0
    Bob | Salary: 25000
    
    Carol is managing a team of 5 people.
    Bonus: 10000.0
    Carol | Salary: 50000 | Team Size: 5
    
    
