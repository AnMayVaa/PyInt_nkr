# OOP — Class & Object
### 📘 Content Notebook
---

## 1. Class & Object
A class is a blueprint. An object is the real thing built from it.


```python
# A class is just a definition not a real thing yet
class Car:
    pass

# Objects are built from the class each is independent
car1 = Car()    # object 1
car2 = Car()    # object 2 completely separate from car1

print(type(car1))   # <class '__main__.Car'>
print(car1)         # not very readable yet, we'll fix this later
```

## 2. __init__ and self
`__init__` runs automatically when an object is created — use it to set up starting data.  
`self` refers to the object itself.


```python
class Car:
    def __init__(self, brand, color):
        # brand, color → parameters — received from outside, exist only during __init__
        # self.brand, self.color → attributes — stored in the object, exist as long as the object exists
        self.brand = brand
        self.color = color
        self.speed = 0        # no parameter needed — every car starts at zero

car1 = Car("Toyota", "red")
car2 = Car("Honda", "blue")

print(car1.brand)   # Toyota
print(car2.color)   # blue
print(car1.speed)   # 0 — set automatically
```


```python
# Each object keeps its own copy of every attribute
# Changing car1's data doesn't affect car2

car1.speed = 100

print(car1.speed)   # 100
print(car2.speed)   # 0 — untouched
```

## 3. Methods
A method is a function inside a class — it defines what an object can do.  
`self` is always the first parameter — it tells the method which object is calling it.


```python
class Car:
    def __init__(self, brand, color):
        self.brand = brand
        self.color = color
        self.speed = 0

    def accelerate(self):           # self = whichever object calls this
        self.speed += 10
        print(f"{self.brand} speeds up — {self.speed} km/h")

    def brake(self):
        self.speed = 0
        print(f"{self.brand} stops.")

car1 = Car("Toyota", "red")
car2 = Car("Honda", "blue")

car1.accelerate()   # Toyota speeds up — 10 km/h
car1.accelerate()   # Toyota speeds up — 20 km/h
car2.accelerate()   # Honda speeds up — 10 km/h  ← independent from car1
car1.brake()        # Toyota stops.
```


```python
# Methods can also take extra parameters besides self

class Car:
    def __init__(self, brand, color):
        self.brand = brand
        self.color = color
        self.speed = 0

    def accelerate(self, amount):   # amount = how much to speed up
        self.speed += amount
        print(f"{self.brand} speeds up — {self.speed} km/h")

car1 = Car("Toyota", "red")
car1.accelerate(30)   # Toyota speeds up — 30 km/h
car1.accelerate(20)   # Toyota speeds up — 50 km/h
```

## 4. __str__
Controls what shows when you `print()` an object.  
Without it — you get a memory address. With it — you get something readable.


```python
# Without __str__
class Car:
    def __init__(self, brand, color):
        self.brand = brand
        self.color = color
        self.speed = 0

car1 = Car("Toyota", "red")
print(car1)   # <__main__.Car object at 0x...>  ← not useful
```

    <__main__.Car object at 0x000001DAE7E43D10>
    


```python
# With __str__ — called automatically when you print the object
class Car:
    def __init__(self, brand, color):
        self.brand = brand
        self.color = color
        self.speed = 0

    def __str__(self):
        return f"{self.brand} ({self.color}) {self.speed} km/h"

car1 = Car("Toyota", "red")
car2 = Car("Honda", "blue")

print(car1)   # Toyota (red) — 0 km/h
print(car2)   # Honda (blue) — 0 km/h
```

    Toyota (red) 0 km/h
    Honda (blue) 0 km/h
    
