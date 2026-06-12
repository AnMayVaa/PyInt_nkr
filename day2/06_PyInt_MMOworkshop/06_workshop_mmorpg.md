# 🗡️ WORKSHOP — MMORPG Text Adventure
---
สร้างเกม text-based ใน terminal

**กติกา**
- ① Character Creator **บังคับทำทุกคน**
- เลือกอีก **2 ระบบ** จากที่เหลือ
- ไม่ต้องทำครบทุก feature — ขอให้รันได้และแสดงผลใน terminal
- เริ่มจาก ① ก่อนเสมอ ระบบอื่นต่อยอดจากนี้ได้

| ระบบ | ความยาก |
|---|---|
| ① Character Creator | 2/5 |
| ② Save & Load | 3/5 |
| ③ Inventory & Shop | 4/5 |
| ④ Monster Battle | 3/5 |
| ⑤ Quest Log | 2/5 |

---
# 🔧 Quick Reference — random & datetime
สองตัวนี้จะใช้ใน workshop — รันดูก่อนได้เลย


```python
import random

# สุ่มเลขจำนวนเต็มระหว่าง min และ max (รวมทั้งสองฝั่ง)
print(random.randint(1, 10))         # เช่น 7

# สุ่มเลือก 1 อย่างจาก list
print(random.choice(["a", "b", "c"]))  # เช่น "b"

# สุ่มทศนิยมระหว่าง 0.8 ถึง 1.2 — ใช้คำนวณ damage ที่ไม่แน่นอน
multiplier = random.uniform(0.8, 1.2)
damage = int(30 * multiplier)         # attack_power 30 สุ่ม ±20%
print("damage:", damage)
```

    6
    c
    damage: 30
    


```python
from datetime import datetime

# เวลาปัจจุบัน
now = datetime.now()
print(now)                                    # 2025-06-15 10:30:45.123456

# จัดรูปแบบให้อ่านง่าย — ใช้ใน Quest Log
print(now.strftime("%Y-%m-%d %H:%M"))         # 2025-06-15 10:30
```

    2026-06-12 18:17:17.746965
    2026-06-12 18:17
    

---
# ① Character Creator
### บังคับ — 2/5

สร้างตัวละครของตัวเอง เลือกชื่อและ class
แต่ละ class มีค่า stats ต่างกัน

**ต้องมี**
- class `Character` มี `name`, `hp`, `attack_power`, `char_class`
- class `Warrior`, `Mage`, `Archer` ที่ inherit จาก `Character`
- แต่ละ class กำหนด hp และ attack_power ของตัวเองใน `__init__`
- `__str__` แสดง character card ใน terminal

**ตัวอย่าง output**
```
Enter your name: Nakharin
Choose class (warrior/mage/archer): warrior

=== CHARACTER CARD ===
Name   : Nakharin
Class  : Warrior
HP     : 150
Attack : 30
======================
```

**Concepts:** `class` · `__init__` · `__str__` · `inheritance` · `super()`


```python
# ① Character Creator

class Character:
    def __init__(self, name, hp, attack_power, char_class):
        self.name         = name
        self.hp           = hp
        self.attack_power = attack_power
        self.char_class   = char_class

    def __str__(self):
        return (
            f"\n=== CHARACTER CARD ==="
            f"\nName   : {self.name}"
            f"\nClass  : {self.char_class}"
            f"\nHP     : {self.hp}"
            f"\nAttack : {self.attack_power}"
            f"\n======================"
        )

class Warrior(Character):
    def __init__(self, name):
        super().__init__(name, hp=150, attack_power=30, char_class="Warrior")


class Mage(Character):
    def __init__(self, name):
        super().__init__(name, hp=80, attack_power=60, char_class="Mage")


class Archer(Character):
    def __init__(self, name):
        super().__init__(name, hp=110, attack_power=45, char_class="Archer")


# --- main ---
name       = input("Enter your name: ")
char_class = input("Choose class (warrior/mage/archer): ").lower()

if char_class == "warrior":
    player = Warrior(name)
elif char_class == "mage":
    player = Mage(name)
elif char_class == "archer":
    player = Archer(name)
else:
    print("Unknown class — defaulting to Warrior")
    player = Warrior(name)

print(player)
```

    
    === CHARACTER CARD ===
    Name   : Pitak
    Class  : Mage
    HP     : 80
    Attack : 60
    ======================
    

---
# ② Save & Load
### เลือกทำ — 3/5

บันทึกตัวละครลงไฟล์ .json และโหลดกลับมาได้

**ต้องมี**
- `save_character(player)` — บันทึก dict ของตัวละครลง `save.json`
- `load_character()` — โหลดกลับมาและสร้าง object ใหม่
- มี error handling ถ้าไฟล์ไม่มีอยู่

**ตัวอย่าง output**
```
Character saved!

Loading save...
=== CHARACTER CARD ===
Name   : Nakharin
Class  : Warrior
...
```

**Concepts:** `json.dump` · `json.load` · `os.path.exists` · `try/except`


```python
# ② Save & Load
import json
import os

def save_character(player):
    # TODO: แปลง player เป็น dict แล้ว dump ลง save.json
    data = {
        "name":         player.name,
        "hp":           player.hp,
        "attack_power": player.attack_power,
        "char_class":   player.char_class
    }
    with open("save.json", "w") as f:
        json.dump(data, f)
        print("Character saved!\n")


def load_character():
    # TODO: โหลด save.json แล้วสร้าง Character object กลับมา
    print("Loading save...")
    # ถ้าไม่มีไฟล์ให้ print แจ้งเตือน
    if not os.path.exists("save.json"):
        print("No save file found.")
        return None
    with open("save.json", "r") as f:
        data = json.load(f)
        char_class = data["char_class"]
        if char_class == "Warrior":
            return Warrior(data["name"])
        elif char_class == "Mage":
            return Mage(data["name"])
        elif char_class == "Archer":
            return Archer(data["name"])
        else:
            print("Unknown character class in save file.")
            return None

# --- test ---
save_character(player)
loaded = load_character()
if loaded:
    print(loaded)
```

    Character saved!
    
    Loading save...
    
    === CHARACTER CARD ===
    Name   : Pitak
    Class  : Mage
    HP     : 80
    Attack : 60
    ======================
    

---
# ③ Inventory & Shop
### เลือกทำ — 4/5

ระบบ inventory และร้านค้า ซื้อของด้วย gold

**ต้องมี**
- class `Item` มี `name`, `item_type`, `effect` (ตัวเลข), `price`
- ตัวละครมี `gold` และ `inventory` (list of Item)
- method `buy(item)` — ถ้า gold พอ ลด gold และเพิ่ม item ใน inventory
- แสดง inventory และ gold ได้
- บันทึก inventory ลงไฟล์ได้ (optional)

**ตัวอย่าง output**
```
=== SHOP ===
1. Health Potion  (heal +50)   — 30 gold
2. Iron Sword     (attack +20) — 80 gold

Your gold: 100
Choose item (1/2): 1
Bought Health Potion!

=== INVENTORY ===
- Health Potion (heal +50)
```

**Concepts:** `class` · `list of objects` · `__str__` · `file` (optional)


```python
# ③ Inventory & Shop
class Item:
    def __init__(self, name, item_type, effect, price):
        self.name      = name
        self.item_type = item_type   # "heal" or "attack"
        self.effect    = effect
        self.price     = price

    def __str__(self):
        return f"{self.name} ({self.item_type} +{self.effect})"

# TODO: เพิ่ม gold และ inventory ให้ Character
class Character:
    def __init__(self, name, hp, attack_power, char_class):
        self.name         = name
        self.hp           = hp
        self.attack_power = attack_power
        self.char_class   = char_class
        self.gold         = 100  # เริ่มต้นมีเงิน 100 gold
        self.inventory    = []   # เริ่มต้นมีของใน inventory ว่าง
# แล้วเขียน buy() method
    def buy(self, item):
        if self.gold >= item.price:
            self.gold -= item.price
            self.inventory.append(item)
            print(f"Bought {item.name} for {item.price} gold. Remaining gold: {self.gold}")
        else:
            print(f"Not enough gold to buy {item.name}. You have {self.gold} gold.")

class Warrior(Character):
    def __init__(self, name):
        super().__init__(name, hp=150, attack_power=30, char_class="Warrior")
    
class Mage(Character):
    def __init__(self, name):
        super().__init__(name, hp=80, attack_power=60, char_class="Mage")

class Archer(Character):
    def __init__(self, name):
        super().__init__(name, hp=110, attack_power=45, char_class="Archer")

# แล้วสร้างร้านค้าและทดสอบ
class Shop:
    def __init__(self):
        self.items = [
            Item("1. Small Potion", "heal", 20, 10),
            Item("2. Large Potion", "heal", 50, 25),
            Item("3. Iron Sword", "attack", 10, 30),
            Item("4. Steel Sword", "attack", 20, 60)
        ]

    def display_items(self):
        print("\n--- SHOP ITEMS ---")
        for idx, item in enumerate(self.items, start=1):
            print(f"{idx}. {item} - {item.price} gold")
        print("------------------")

#save and load
def save_character(player):
    # TODO: แปลง player เป็น dict แล้ว dump ลง save.json
    data = {
        "name":         player.name,
        "hp":           player.hp,
        "attack_power": player.attack_power,
        "char_class":   player.char_class,
        "gold":         player.gold,
        "inventory":    [(item.name, item.item_type, item.effect, item.price) for item in player.inventory]
    }
    with open("save.json", "w") as f:
        json.dump(data, f)
        print("Character saved!\n")


def load_character():
    # TODO: โหลด save.json แล้วสร้าง Character object กลับมา
    print("Loading save...")
    # ถ้าไม่มีไฟล์ให้ print แจ้งเตือน
    if not os.path.exists("save.json"):
        print("No save file found.")
        return None
    with open("save.json", "r") as f:
        data = json.load(f)
        char_class = data["char_class"]
        if char_class == "Warrior":
            return Warrior(data["name"])
        elif char_class == "Mage":
            return Mage(data["name"])
        elif char_class == "Archer":
            return Archer(data["name"])
        else:
            print("Unknown character class in save file.")
            return None

# --- test shop ---
player = Mage("Pitak")
shop = Shop()
shop.display_items()
print(f"\nYour gold: {player.gold}")
try:
    choice = int(input("Enter the number of the item you want to buy: "))
    if 1 <= choice <= len(shop.items):
        selected_item = shop.items[choice - 1]
        player.buy(selected_item)
    else:
        print("Invalid choice.")
except ValueError:
    print("Please enter a valid number.")
finally:    
    print(f"\nYour inventory: {[str(item) for item in player.inventory]}")

save_character(player)

```

    
    --- SHOP ITEMS ---
    1. 1. Small Potion (heal +20) - 10 gold
    2. 2. Large Potion (heal +50) - 25 gold
    3. 3. Iron Sword (attack +10) - 30 gold
    4. 4. Steel Sword (attack +20) - 60 gold
    ------------------
    
    Your gold: 100
    Bought 1. Small Potion for 10 gold. Remaining gold: 90
    
    Your inventory: ['1. Small Potion (heal +20)']
    Character saved!
    
    

---
# ④ Monster Battle
### เลือกทำ — 3/5

สู้กับมอนสเตอร์สุ่ม แสดง log แต่ละ round

**ต้องมี**
- class `Monster` มี `name`, `hp`, `attack_power`
- class `Goblin`, `Orc`, `Dragon` inherit จาก Monster
- ฟังก์ชัน `battle(player, monster)` — วน loop สู้จนฝ่ายใดฝ่ายหนึ่ง hp หมด
- สุ่ม damage แต่ละ round ด้วย random
- แสดง log ทุก round

**ตัวอย่าง output**
```
=== BATTLE START ===
Nakharin vs Goblin

Round 1
Nakharin attacks for 28 damage — Goblin HP: 22
Goblin attacks for 12 damage   — Nakharin HP: 138

Round 2
Nakharin attacks for 31 damage — Goblin HP: 0

Nakharin wins!
```

**Concepts:** `inheritance` · `override` · `random` · `while loop`


```python
# ④ Monster Battle
import random

# TODO: เพิ่ม is_alive()
class Character:
    def __init__(self, name, hp, attack_power, char_class):
        self.name         = name
        self.hp           = hp
        self.attack_power = attack_power
        self.char_class   = char_class

    def is_alive(self):
        return self.hp > 0
    
    def __str__(self):
        return (
            f"\n=== CHARACTER CARD ==="
            f"\nName   : {self.name}"
            f"\nClass  : {self.char_class}"
            f"\nHP     : {self.hp}"
            f"\nAttack : {self.attack_power}"
            f"\n======================"
        )

class Warrior(Character):
    def __init__(self, name):
        super().__init__(name, hp=150, attack_power=30, char_class="Warrior")
    
class Mage(Character):
    def __init__(self, name):
        super().__init__(name, hp=80, attack_power=60, char_class="Mage")

class Archer(Character):
    def __init__(self, name):
        super().__init__(name, hp=110, attack_power=45, char_class="Archer")

# Monster class และ subclass
class Monster:
    def __init__(self, name, hp, attack_power):
        self.name         = name
        self.hp           = hp
        self.attack_power = attack_power

    def is_alive(self):
        return self.hp > 0

    def __str__(self):
        return f"{self.name} (HP: {self.hp})"

class Goblin(Monster):
    def __init__(self):
        super().__init__("Goblin", hp=50, attack_power=15)

class Orc(Monster):
    def __init__(self):
        super().__init__("Orc", hp=100, attack_power=25)

class Dragon(Monster):
    def __init__(self):
        super().__init__("Dragon", hp=200, attack_power=50)


def battle(player, monster):
    # TODO: เขียน battle loop
    round = 1
    while player.is_alive() and monster.is_alive():
        print(f"--- Round {round} ---")
        # Player attacks monster
        player_multiplier = random.uniform(0.8, 1.2) # แต่ละ round สุ่ม damage ±20% จาก attack_power
        player_damage = int(player.attack_power * player_multiplier)
        monster.hp -= player_damage
        print(f"{player.name} attacks {monster.name} for {player_damage} damage! {monster}") # แสดง log ทุก round

        if not monster.is_alive(): # จบเมื่อฝ่ายใดฝ่ายหนึ่ง hp <= 0
            print(f"{monster.name} is defeated!") # แสดง log ทุก round
            break

        # Monster attacks player
        monster_multiplier = random.uniform(0.8, 1.2) # แต่ละ round สุ่ม damage ±20% จาก attack_power
        monster_damage = int(monster.attack_power * monster_multiplier)
        player.hp -= monster_damage
        print(f"{monster.name} attacks {player.name} for {monster_damage} damage! {player}") # แสดง log ทุก round

        if not player.is_alive(): # จบเมื่อฝ่ายใดฝ่ายหนึ่ง hp <= 0
            print(f"{player.name} is defeated!") # แสดง log ทุก round
            break
        
        round += 1

# --- test ---
player = Mage("Pitak")
monsters = [Goblin(), Orc(), Dragon()]
enemy    = random.choice(monsters)
battle(player, enemy)
```

    --- Round 1 ---
    Pitak attacks Orc for 52 damage! Orc (HP: 48)
    Orc attacks Pitak for 27 damage! 
    === CHARACTER CARD ===
    Name   : Pitak
    Class  : Mage
    HP     : 53
    Attack : 60
    ======================
    --- Round 2 ---
    Pitak attacks Orc for 68 damage! Orc (HP: -20)
    Orc is defeated!
    

---
# ⑤ Quest Log
### เลือกทำ — 2/5

บันทึกและอ่านประวัติ quest ที่ทำสำเร็จ

**ต้องมี**
- `add_quest(quest_name)` — บันทึก quest ลง `questlog.txt` พร้อม timestamp
- `show_quests()` — อ่านและแสดงประวัติ quest ทั้งหมด
- มี error handling ถ้าไฟล์ยังไม่มี

**ตัวอย่าง output**
```
Quest completed: Defeat the Goblin
Quest completed: Find the lost sword

=== QUEST LOG ===
[2025-06-15 10:30] Defeat the Goblin
[2025-06-15 10:45] Find the lost sword
```

**Concepts:** `file write` · `append` · `read` · `exception` · `datetime`


```python
# ⑤ Quest Log
from datetime import datetime

def add_quest(quest_name):
    # TODO: บันทึก quest_name พร้อม timestamp ลง questlog.txt
    timestamp = datetime.now().strftime("%Y-%m-%d %H:%M")
    with open("questlog.txt", "a") as f:
        f.write(f"{timestamp} - {quest_name}\n")

def show_quests():
    # TODO: อ่าน questlog.txt แล้วแสดงผล
    # ถ้าไฟล์ไม่มีให้ print แจ้งเตือน
    try:
        with open("questlog.txt", "r") as f:
            quests = f.readlines()
            if quests:
                for quest in quests:
                    print(quest.strip())
            else:
                print("No quests found.")
    except FileNotFoundError:
        print("Quest log file not found.")

# --- test ---
add_quest("Defeat the Goblin")
add_quest("Find the lost sword")
show_quests()
```

    2026-06-12 18:25 - Defeat the Goblin
    2026-06-12 18:25 - Find the lost sword
    
