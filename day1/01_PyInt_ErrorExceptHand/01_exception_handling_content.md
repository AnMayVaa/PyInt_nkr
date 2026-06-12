# Exception & Error Handling
### 📘 Content Notebook
---

## 1. try / except
Put risky code inside `try` if it fails, `except` catches it.


```python
# Basic try/except
# Try running this then change input to 'abc' and run again

try:
    age = int(input("Enter your age: "))  # this might fail
    print("Your age is", age)

except ValueError:                        # if it fails with ValueError
    print("Please enter a number!")       # do this instead
```

    Your age is 123
    

## 2. Common Exceptions
These are the most common exceptions you'll encounter.


```python
# ValueError wrong value for the type
try:
    int("John")
except ValueError as e:
    print("ValueError:", e)
```

    ValueError: invalid literal for int() with base 10: 'John'
    


```python
# TypeError wrong type entirely
try:
    "age: " + 25
except TypeError as e:
    print("TypeError:", e)
```

    TypeError: can only concatenate str (not "int") to str
    


```python
# ZeroDivisionError dividing by zero
try:
    10 / 0
except ZeroDivisionError as e:
    print("ZeroDivisionError:", e)
```


```python
# FileNotFoundError file doesn't exist
try:
    open("ghost.txt")
except FileNotFoundError as e:
    print("FileNotFoundError:", e)
```

    FileNotFoundError: [Errno 2] No such file or directory: 'ghost.txt'
    


```python
# KeyError key not found in dict
try:
    data = {"name": "Alice"}
    data["name"]
except KeyError as e:
    print("KeyError:", e)
```

    KeyError: 'email'
    


```python
# IndexError index out of range
try:
    colors = ["red", "green", "blue"]
    colors[99]
except IndexError as e:
    print("IndexError:", e)
```


```python
# NameError — variable not defined
try:
    print(score)
except NameError as e:
    print("NameError:", e)
```


```python
# AttributeError — object has no attribute
try:
    None.upper()
except AttributeError as e:
    print("AttributeError:", e)
```

## 3. Multiple Except Blocks
Each `except` catches one specific exception — Python runs the first one that matches.


```python
# Try: input 'abc' → ValueError
# Try: input '0'   → ZeroDivisionError
# Try: input '4'   → success

try:
    s = input("Enter an integer to divide 100 by: ")
    num = int(s)                    # might raise ValueError
    result = 100 / num              # might raise ZeroDivisionError
    print("100 /", num, "=", result)

except ValueError:
    print("Invalid input: please enter a whole number.")

except ZeroDivisionError:
    print("Math error: cannot divide by zero.")
```

## 4. else / finally
- `else` runs only when try succeeds with no exception
- `finally` always runs, no matter what


```python
# Try: input 'abc' → except runs, else skipped, finally runs
# Try: input '0'   → except runs, else skipped, finally runs
# Try: input '4'   → else runs, finally runs

try:
    s = input("Enter an integer to divide 100 by: ")
    num = int(s)
    result = 100 / num
    print("100 /", num, "=", result)

except ValueError:
    print("Invalid input: please enter a whole number.")

except ZeroDivisionError:
    print("Math error: cannot divide by zero.")

else:
    print("No exception — calculation succeeded!")  # only if try passed

finally:
    print("Done.")                                  # always runs
```

## 5. Capturing the Error Message — as e
`as e` stores the error message so you can print or use it.


```python
# Without as e — you know something went wrong, but not what
try:
    int("abc")
except ValueError:
    print("Something went wrong.")
```


```python
# With as e — you get the full error message from Python
try:
    int("abc")
except ValueError as e:
    print("Error:", e)
```

## 6. raise
Sometimes you need to trigger an exception yourself — not wait for Python to do it.


```python
# raise lets you set your own rules
# If the input breaks them — you throw the exception yourself

def set_age(age):
    if age < 0:
        raise ValueError("Age cannot be negative.")  # your own rule
    return age

try:
    set_age(-5)
except ValueError as e:
    print("Error:", e)
```

## 7. Reading a Traceback
When a crash happens, Python gives you a traceback.
**Always read the last line first — then trace upward.**


```python
# Run this and read the traceback carefully
# Last line tells you WHAT went wrong
# Lines above tell you WHERE it happened

def calculate(n):
    return 100 / n

calculate(0)
```
