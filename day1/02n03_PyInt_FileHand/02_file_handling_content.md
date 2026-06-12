# File Handling + JSON
### 📘 Content Notebook
---

## 1. with statement
The recommended way to open files — closes automatically, even if something crashes.


```python
# Without with — you must close manually
f = open("london_bridge.txt", "r")   # default mode is "r"
content = f.read()
print(content)
f.close()                    # easy to forget — risky if crash happens before this
```

    London Bridge is falling down,
    Falling down, falling down,
    London Bridge is falling down,
    My fair lady.
    
    


```python
# With with — closes automatically when block ends
with open("london_bridge.txt", "r") as f:   # default mode is "r"
    content = f.read()
    print(content)
# file is already closed here — no extra step needed
```

    London Bridge is falling down,
    Falling down, falling down,
    London Bridge is falling down,
    My fair lady.
    
    

## 2. Writing a File
Write data to disk so it survives after the program stops.


```python
# "w" — overwrite — starts fresh every time
# if file doesn't exist → creates it
# if file already exists → deletes everything first

with open("data.txt", "w") as f:
    f.write("Hello\n")    # \n = new line — without it everything is on one line
    f.write("World\n")

print("File written.")
```

    File written.
    


```python
# "a" — append — adds to the end, never deletes existing content
# run this cell multiple times and see what happens

with open("data.txt", "a") as f:
    f.write("One more line\n")

print("Line appended.")
```

    Line appended.
    

## 3. Reading a File
Three ways to read — each works differently.


```python
# read() — reads entire file as one big string
with open("data.txt", "r") as f:
    content = f.read()

print(type(content))   # <class 'str'>
print(content)
```

    <class 'str'>
    Hello
    World
    One more line
    
    


```python
# readline() — reads one line per call, cursor moves forward each time
with open("data.txt", "r") as f:
    line1 = f.readline()   # reads first line
    line2 = f.readline()   # reads second line

print(line1)
print(line2)
```

    Hello
    
    Hi there!
    World
    
    Hi there!
    


```python
# readlines() — reads all lines, returns a list
with open("data.txt", "r") as f:
    lines = f.readlines()

print(type(lines))    # <class 'list'>
print(lines)          # ['Hello\n', 'World\n', ...]
print(lines[0])       # first line
```

    <class 'list'>
    ['Hello\n', 'World\n', 'One more line\n']
    Hello
    
    

## 4. seek() — moving the cursor
`seek(0)` moves the cursor back to the beginning — so you can read again without reopening.


```python
with open("data.txt", "r") as f:
    first_read = f.read()    # reads everything, cursor now at the end
    
    f.seek(0)                # reset cursor back to the beginning
    
    second_read = f.read()   # reads everything again from the start

print("First read:")
print(first_read)
print("Second read:")
print(second_read)
```

    First read:
    Hello
    World
    One more line
    
    Second read:
    Hello
    World
    One more line
    
    

## 5. os.path
Check if a file exists before opening — prevents crashes.


```python
import os

# exists() — returns True if file exists, False if not
print(os.path.exists("data.txt"))    # True  — file we just created
print(os.path.exists("ghost.txt"))   # False — file that doesn't exist
```

    True
    False
    


```python
# Check before opening — safe pattern
filename = "data.txt"

if os.path.exists(filename):
    with open(filename, "r") as f:
        print(f.read())
else:
    print(f"File '{filename}' not found.")
```

    File 'data.txt' not found.
    


```python
# join() — safely joins path for any OS
# Windows uses \ but Mac/Linux uses /
# join() picks the right one automatically

path = os.path.join("folder", "data.txt")
print(path)   # folder/data.txt (Mac) or folder\data.txt (Windows)
```

    folder\data.txt
    

## 6. JSON — json.dump
Convert a Python dict and write it to a `.json` file.


```python
import json

student = {
    "name": "Alice",
    "score": 85,
    "passed": True
}

with open("student.json", "w", encoding="utf-8") as f:  # utf-8 required for Thai
    json.dump(student, f,
              ensure_ascii=False,   # keep Thai characters readable, not \u escape codes
              indent=2)             # add spaces so humans can read the file

print("Saved to student.json")
```

    Saved to student.json
    

## 7. JSON — json.load
Read a `.json` file and convert it back to a Python dict.


```python
with open("student.json", "r", encoding="utf-8") as f:
    data = json.load(f)   # returns a Python dict — ready to use immediately

print(type(data))          # <class 'dict'>
print(data["name"])        # Alice
print(data["score"])       # 85
print(data["passed"])      # True  ← true in JSON becomes True in Python
```

## 📝 Note — encoding vs ensure_ascii

**`encoding="utf-8"`** → tells Python which character set to use **when writing/reading the file**  
Without it — Windows uses its own default encoding → Thai characters may break when opened elsewhere

**`ensure_ascii=False`** → tells `json.dump` **not to convert** non-English characters before writing  
- Default (`True`) → `"สวัสดี"` becomes `"\u0e2a\u0e27\u0e31\u0e2a\u0e14\u0e35"` — unreadable  
- `False` → `"สวัสดี"` stays `"สวัสดี"` — then `encoding` handles the rest

**Both are needed** — `ensure_ascii=False` keeps characters as-is, `encoding="utf-8"` makes sure the file can store them correctly.
