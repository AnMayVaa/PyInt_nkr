# OOP — Inheritance & Polymorphism
### 📘 Content Notebook
---

## 1. Inheritance
A child class inherits everything from its parent — you only write what's new or different.


```python
# Parent class
class Car:
    def __init__(self, brand, color):
        self.brand = brand
        self.color = color
        self.speed = 0

    def accelerate(self):
        self.speed += 10
        print(f"{self.brand} speeds up — {self.speed} km/h")

    def describe(self):
        print(f"{self.brand} runs on fuel")


# Child class — inherits everything from Car
class ElectricCar(Car):
    def __init__(self, brand, color, battery):
        super().__init__(brand, color)  # run Car's __init__ first — sets brand, color, speed
        self.battery = battery          # then add what's new

    def charge(self):                   # new method — only ElectricCar has this
        self.battery = 100
        print(f"{self.brand} fully charged.")


ev = ElectricCar("Tesla", "white", 80)
ev.accelerate()    # inherited from Car — no need to rewrite
ev.charge()        # ElectricCar only
print(ev.speed)    # attribute from Car — still accessible
```

## 2. Override & Polymorphism
Override: child rewrites a parent's method.  
Polymorphism: same method call, different result depending on the object.


```python
class Car:
    def __init__(self, brand, color):
        self.brand = brand
        self.color = color
        self.speed = 0

    def describe(self):
        print(f"{self.brand} runs on fuel")


class ElectricCar(Car):
    def __init__(self, brand, color, battery):
        super().__init__(brand, color)
        self.battery = battery

    def describe(self):                       # override — replaces Car's describe()
        print(f"{self.brand} runs on battery ({self.battery}%)")


vehicles = [
    Car("Toyota", "red"),
    ElectricCar("Tesla", "white", 80),
    ElectricCar("BMW", "black", 60),
]

for v in vehicles:
    v.describe()    # polymorphism — same call, different result per object
```

    Toyota runs on fuel
    Tesla runs on battery (80%)
    BMW runs on battery (60%)
    

## 3. super() — calling the parent's method
`super()` lets you call the parent's version of a method — useful when you want to extend, not fully replace.


```python
class Car:
    def __init__(self, brand, color):
        self.brand = brand
        self.color = color
        self.speed = 0

    def describe(self):
        print(f"{self.brand} ({self.color})")


class ElectricCar(Car):
    def __init__(self, brand, color, battery):
        super().__init__(brand, color)
        self.battery = battery

    def describe(self):
        super().describe()                    # call parent's describe() first
        print(f"Battery: {self.battery}%")   # then add more


ev = ElectricCar("Tesla", "white", 80)
ev.describe()
# Tesla (white)
# Battery: 80%
```

    Tesla (white)
    Battery: 80%
    
