# 第 12 章｜物件導向基礎

## 學習目標

- 理解物件導向程式設計的概念
- 掌握類別（Class）與物件（Object）的定義
- 學會建立屬性與方法
- 理解封裝、繼承、多型的概念

---

## 12.1 什麼是物件導向？

> **📝 Note（說明）**：**物件導向程式設計（OOP）** 是一種將程式視為「物件」組成的設計方法，每個物件包含屬性（資料）和方法（行為）。

**物件導向程式設計（OOP）** 是一種將程式視為「物件」組成的設計方法。

```
類別（Class）→ 藍圖/模板
物件（Object）→ 根據藍圖產生的實體
```

### 生活中的例子

```
類別：人類
物件：张三、李四、王五（每個人都是人類的實例）

人類具有：
- 屬性：姓名、年齡、性別
- 方法：吃飯、睡覺、說話
```

---

## 12.2 建立類別

> **💡 Tip（小技巧）**：類別名稱通常使用 PascalCase（每個單字首字母大寫），例如 `Person`、`Dog`、`BankAccount`。

### 基本語法

```python
class Person:
    """人類"""
    
    # 初始化方法（建構函式）
    def __init__(self, name, age):
        """初始化物件屬性"""
        self.name = name    # 屬性
        self.age = age
    
    # 方法
    def greet(self):
        return f"你好，我叫{self.name}"

# 建立物件
person1 = Person("小明", 20)
person2 = Person("小華", 25)

print(person1.name)   # 小明
print(person1.greet()) # 你好，我叫小明
```

---

## 12.3 屬性與方法

> **📝 Note（說明）**：實例屬性屬於每個物件（實例），而類別屬性則是該類別所有物件共有的。

### 實例屬性

```python
class Dog:
    def __init__(self, name, age):
        self.name = name    # 實例屬性
        self.age = age
    
    def bark(self):        # 方法
        return f"{self.name} 說：汪汪！"

# 建立物件
dog = Dog("小白", 3)
print(dog.name)
print(dog.bark())
```

### 類別屬性

```python
class Dog:
    species = "狗"         # 類別屬性（所有物件共用）
    
    def __init__(self, name):
        self.name = name    # 實例屬性

dog1 = Dog("小白")
dog2 = Dog("小黑")

print(dog1.species)   # 狗
print(dog2.species)   # 狗
Dog.species = "犬類"  # 改變類別屬性
print(dog1.species)   # 犬類
```

---

## 12.4 self 的意義

`self` 代表物件本身，類似於中文的「自己」：

```python
class Person:
    def __init__(self, name):
        self.name = name
    
    def greet(self):
        # self 就是「自己」
        return f"你好，我是{self.name}"

p = Person("小明")
# p.greet() 相當於 Person.greet(p)
```

---

## 12.5 封裝

> **⚠️ Caution（注意）**：Python 沒有真正的私有屬性，使用雙底線前綴（`__balance`）會進行名稱修飾，但仍然可以透過 `_ClassName__attribute` 訪問。封裝主要是提醒開發者哪些屬性不應該直接從外部修改。

### 公開與私有

```python
class BankAccount:
    def __init__(self, balance):
        self.balance = balance          # 公開屬性
        self._balance = balance         #  Convention：私有（但仍可存取）
        self.__balance = balance        # 名稱修飾（偽私有）
    
    def deposit(self, amount):
        if amount > 0:
            self.__balance += amount
            return True
        return False
    
    def withdraw(self, amount):
        if amount <= self.__balance:
            self.__balance -= amount
            return True
        return False
    
    def get_balance(self):
        return self.__balance

account = BankAccount(1000)
account.deposit(500)
print(account.get_balance())  # 1500
```

---

## 12.6 繼承

> **💡 Tip（小技巧）**：繼承讓你可以重用父類別的程式碼，同時可以覆寫（override）或擴充父類別的方法，這是物件導向程式設計的核心概念之一。

### 基本語法

```python
# 父類別
class Animal:
    def __init__(self, name):
        self.name = name
    
    def speak(self):
        pass

# 子類別
class Dog(Animal):          # 繼承 Animal
    def speak(self):
        return f"{self.name} 說：汪汪！"

class Cat(Animal):
    def speak(self):
        return f"{self.name} 說：喵喵！"

dog = Dog("小白")
print(dog.speak())  # 小白 說：汪汪！
```

### super() 函式

```python
class Person:
    def __init__(self, name):
        self.name = name

class Student(Person):
    def __init__(self, name, grade):
        super().__init__(name)  # 呼叫父類別的 __init__
        self.grade = grade

student = Student("小明", "大一")
print(student.name)   # 小明
print(student.grade)  # 大一
```

---

## 12.7 多型

> **📝 Note（說明）**：**多型（Polymorphism）** 允許不同類別的物件對同一訊息（方法呼叫）做出不同的回應。這使得程式碼更具彈性和可擴充性。

同一個方法，不同物件有不同行為：

```python
class Animal:
    def speak(self):
        pass

class Dog(Animal):
    def speak(self):
        return "汪汪"

class Cat(Animal):
    def speak(self):
        return "喵喵"

class Duck(Animal):
    def speak(self):
        return "嘎嘎"

# 多型：相同的方法，不同行為
animals = [Dog(), Cat(), Duck()]
for animal in animals:
    print(animal.speak())
```

---

## 12.8 Turtle 繪圖：用類別設計圖形

學會了物件導向，我們可以用類別來設計各種圖形，讓程式碼更有結構！

### 設計圓形類別

```python
import turtle

class Circle:
    def __init__(self, x, y, radius, color):
        self.x = x
        self.y = y
        self.radius = radius
        self.color = color
    
    def draw(self):
        turtle.penup()
        turtle.goto(self.x, self.y)
        turtle.pendown()
        turtle.color(self.color)
        turtle.circle(self.radius)

# 建立多個圓形物件
c1 = Circle(-100, 0, 50, "red")
c2 = Circle(0, 0, 50, "green")
c3 = Circle(100, 0, 50, "blue")

# 畫出所有圓形
c1.draw()
c2.draw()
c3.draw()

turtle.done()
```

### 設計多邊形類別

```python
import turtle

class Polygon:
    def __init__(self, x, y, sides, length, color):
        self.x = x
        self.y = y
        self.sides = sides
        self.length = length
        self.color = color
    
    def draw(self):
        turtle.penup()
        turtle.goto(self.x, self.y)
        turtle.pendown()
        turtle.color(self.color)
        
        angle = 360 / self.sides
        for i in range(self.sides):
            turtle.forward(self.length)
            turtle.right(angle)

# 建立不同多邊形
triangle = Polygon(-150, 50, 3, 80, "red")
square = Polygon(-50, 50, 4, 60, "green")
pentagon = Polygon(50, 50, 5, 50, "blue")
hexagon = Polygon(150, 50, 6, 40, "purple")

# 畫出所有多邊形
triangle.draw()
square.draw()
pentagon.draw()
hexagon.draw()

turtle.done()
```

### 練習：設計自己的圖形類別

```python
import turtle

class Star:
    def __init__(self, x, y, size, color):
        self.x = x
        self.y = y
        self.size = size
        self.color = color
    
    def draw(self):
        turtle.penup()
        turtle.goto(self.x, self.y)
        turtle.pendown()
        turtle.color(self.color)
        
        for i in range(5):
            turtle.forward(self.size)
            turtle.right(144)

# 畫出星星家族
star1 = Star(0, 50, 50, "yellow")
star2 = Star(-100, -50, 30, "gold")
star3 = Star(100, -50, 30, "gold")

star1.draw()
star2.draw()
star3.draw()

turtle.done()
```

---

## 12.9 實用範例

### 範例1：學生管理系統

```python
class Student:
    def __init__(self, name, student_id):
        self.name = name
        self.student_id = student_id
        self.scores = []
    
    def add_score(self, score):
        if 0 <= score <= 100:
            self.scores.append(score)
            return True
        return False
    
    def get_average(self):
        if not self.scores:
            return 0
        return sum(self.scores) / len(self.scores)
    
    def __str__(self):
        return f"{self.name} ({self.student_id})"

# 使用
s1 = Student("小明", "A123456")
s1.add_score(85)
s1.add_score(90)
s1.add_score(78)

print(s1)                    # 小明 (A123456)
print(f"平均：{s1.get_average():.1f}")  # 平均：84.3
```

### 範例2：銀行帳戶系統

```python
class BankAccount:
    def __init__(self, account_no, initial_balance=0):
        self.__account_no = account_no
        self.__balance = initial_balance
    
    def deposit(self, amount):
        if amount > 0:
            self.__balance += amount
            return True
        return False
    
    def withdraw(self, amount):
        if amount > 0 and amount <= self.__balance:
            self.__balance -= amount
            return True
        return False
    
    def get_balance(self):
        return self.__balance
    
    def __str__(self):
        return f"帳戶 {self.__account_no}，餘額：{self.__balance}"

class SavingsAccount(BankAccount):
    def __init__(self, account_no, initial_balance=0, interest_rate=0.02):
        super().__init__(account_no, initial_balance)
        self.interest_rate = interest_rate
    
    def add_interest(self):
        interest = self.get_balance() * self.interest_rate
        self.deposit(interest)

# 使用
account = SavingsAccount("123-456-789", 10000, 0.02)
print(account)
account.deposit(5000)
account.add_interest()
print(account.get_balance())  # 15300
```

---

## 本章小結

| 概念 | 說明 |
|------|------|
| 類別 | 定義物件的模板 |
| 物件 | 類別的實例 |
| 屬性 | 物件的資料 |
| 方法 | 物件的函式 |
| 繼承 | 子類別取得父類別的屬性和方法 |
| 封裝 | 隱藏內部細節 |
| 多型 | 同一方法，不同行為 |

---

## 練習題

### 基礎題

1. **人類別**：建立 Person 類別，包含姓名和年齡屬性，以及打招呼方法。
2. **矩形類別**：建立 Rectangle 類別，計算面積和周長。
3. **繼承練習**：建立 Student 類別繼承 Person。
4. **點類別**：建立 Point 類別，包含 x, y 座標。
5. **書籍類別**：建立 Book 類別，包含書名、作者、價格。
6. **方法呼叫**：在類別中建立多個方法並練習呼叫。
7. **類別屬性**：建立類別屬性並在類別和物件中存取。
8. **__str__ 方法**：實作 __str__ 方法自訂輸出格式。
9. **靜態方法**：建立靜態方法並練習呼叫。
10. **簡單計算機類別**：建立 Calculator 類別，實作加减乘除方法。

### 進階題

1. **形狀類別**：建立 Shape 父類別，以及 Circle、Rectangle 子類別。
2. **車輛系統**：建立 Vehicle、Car、Motorcycle 類別。
3. **帳戶管理**：建立 Account 類別，實作存款、提款功能。
4. **圖書館系統**：建立 Book、Member、Library 類別。
5. **遊戲角色**：建立 RPG 遊戲的角色系統。
6. **多重繼承**：建立同時繼承多個類別的子類別。
7. **多型應用**：使用多型讓不同類別執行相同方法。
8. **抽象類別**：建立抽象類別並實作具體子類別。

### 挑戰題

1. **醫院管理系統**：建立病人、醫生、護士、病房等類別。
2. **電子商務系統**：建立商品、購物車、訂單、使用者類別。
3. **航空公司系統**：建立航班、乘客、機票類別。

---

## 12.7 實用範例 - 小遊戲

### 遊戲 1：寶可夢戰鬥系統（OOP版）

使用物件導向設計的寶可夢戰鬥遊戲！

```python
# 寶可夢戰鬥系統（OOP版）
# 學習重點：類別設計、繼承、多型

import random

class Pokemon:
    """寶可夢基礎類別"""
    
    def __init__(self, name, hp, attack, defense, skill):
        self.name = name
        self.max_hp = hp
        self.hp = hp
        self.attack = attack
        self.defense = defense
        self.skill = skill
    
    def attack_enemy(self, enemy):
        """攻擊敵人"""
        damage = max(1, self.attack - enemy.defense // 2)
        damage = damage + random.randint(-3, 3)
        enemy.hp = max(0, enemy.hp - damage)
        return damage
    
    def is_alive(self):
        """是否存活"""
        return self.hp > 0
    
    def show_info(self):
        """顯示資訊"""
        return f"{self.name}: {self.hp}/{self.max_hp} HP"

class FirePokemon(Pokemon):
    """火屬性寶可夢"""
    def __init__(self, name, hp, attack, defense, skill):
        super().__init__(name, hp, attack, defense, skill)
        self.type = "火"
    
    def special_attack(self, enemy):
        """特殊攻擊"""
        print(f"🔥 {self.name} 使用了 {self.skill}！")
        damage = self.attack_enemy(enemy)
        print(f"造成 {damage} 傷害！")
        return damage

class WaterPokemon(Pokemon):
    """水屬性寶可夢"""
    def __init__(self, name, hp, attack, defense, skill):
        super().__init__(name, hp, attack, defense, skill)
        self.type = "水"
    
    def special_attack(self, enemy):
        """特殊攻擊"""
        print(f"💧 {self.name} 使用了 {self.skill}！")
        damage = self.attack_enemy(enemy)
        print(f"造成 {damage} 傷害！")
        return damage

class ElectricPokemon(Pokemon):
    """電屬性寶可夢"""
    def __init__(self, name, hp, attack, defense, skill):
        super().__init__(name, hp, attack, defense, skill)
        self.type = "電"
    
    def special_attack(self, enemy):
        """特殊攻擊"""
        print(f"⚡ {self.name} 使用了 {self.skill}！")
        damage = self.attack_enemy(enemy)
        print(f"造成 {damage} 傷害！")
        return damage

# 建立寶可夢
pokemons = [
    FirePokemon("小火龍", 100, 25, 15, "火花"),
    FirePokemon("火焰馬", 110, 28, 18, "火焰旋風"),
    WaterPokemon("傑尼龜", 120, 20, 22, "水槍"),
    WaterPokemon("水箭龜", 130, 25, 25, "水炮"),
    ElectricPokemon("皮卡丘", 90, 30, 12, "十萬伏特"),
    ElectricPokemon("雷丘", 100, 35, 15, "打雷")
]

# 遊戲
print("=" * 50)
print("      ⚔️ 寶可夢戰鬥（OOP版）⚔️")
print("=" * 50)
print()

# 選擇寶可夢
print("選擇你的寶可夢：")
for i, p in enumerate(pokemons, 1):
    print(f"{i}. {p.name} ({p.type}) - HP:{p.max_hp} ATK:{p.attack}")

player_idx = int(input("\n選擇 (1-6)：")) - 1
player_pokemon = pokemons[player_idx]

# 電腦選擇
available = [i for i in range(len(pokemons)) if i != player_idx]
computer_idx = random.choice(available)
computer_pokemon = pokemons[computer_idx]

print(f"\n你選擇了 {player_pokemon.name}！")
print(f"電腦選擇了 {computer_pokemon.name}！")

# 戰鬥
print("\n⚔️ 戰鬥開始！")
round_num = 1

while player_pokemon.is_alive() and computer_pokemon.is_alive():
    print(f"\n=== 第 {round_num} 回合 ===")
    print(f"{player_pokemon.show_info()} | {computer_pokemon.show_info()}")
    
    # 玩家攻擊
    damage = player_pokemon.special_attack(computer_pokemon)
    print(f"→ {computer_pokemon.name} 剩下 {computer_pokemon.hp} HP")
    
    if not computer_pokemon.is_alive():
        break
    
    # 電腦攻擊
    damage = computer_pokemon.special_attack(player_pokemon)
    print(f"→ {player_pokemon.name} 剩下 {player_pokemon.hp} HP")
    
    round_num += 1

# 結果
print()
print("=" * 50)
if player_pokemon.is_alive():
    print(f"🎉 你獲勝了！")
else:
    print(f"😢 你輸了...")
print("=" * 50)
```

---

### 遊戲 2：卡牌RPG遊戲

使用類別設計的卡牌遊戲！

```python
# 卡牌RPG遊戲
# 學習重點：類別設計、繼承、物件管理

import random

class Card:
    """卡牌類別"""
    def __init__(self, name, card_type, attack, defense, cost):
        self.name = name
        self.card_type = card_type  # "攻擊" 或 "防禦" 或 "法術"
        self.attack = attack
        self.defense = defense
        self.cost = cost
    
    def __str__(self):
        return f"{self.name} ({self.card_type}) ATK:{self.attack} DEF:{self.defense} COST:{self.cost}"

class Player:
    """玩家類別"""
    def __init__(self, name):
        self.name = name
        self.hp = 30
        self.energy = 3
        self.max_energy = 3
        self.hand = []
        self.deck = []
        self.create_deck()
    
    def create_deck(self):
        """建立牌組"""
        cards = [
            # 攻擊卡
            Card("火球術", "攻擊", 6, 0, 2),
            Card("冰凍箭", "攻擊", 4, 0, 1),
            Card("雷擊", "攻擊", 8, 0, 3),
            Card("斬擊", "攻擊", 3, 0, 1),
            Card("風刃", "攻擊", 5, 0, 2),
            # 防禦卡
            Card("盾牌", "防禦", 0, 4, 1),
            Card("護甲", "防禦", 0, 6, 2),
            Card("石牆", "防禦", 0, 8, 3),
            # 法術卡
            Card("治療術", "法術", 0, -5, 2),  # 負攻擊代表治療
            Card("能量爆發", "法術", 3, 0, 1),
        ]
        self.deck = cards * 2  # 牌組有兩倍
        random.shuffle(self.deck)
    
    def draw_card(self, count=1):
        """抽牌"""
        for _ in range(count):
            if self.deck:
                self.hand.append(self.deck.pop())
    
    def show_hand(self):
        """顯示手牌"""
        print(f"\n{self.name} 的手牌：")
        for i, card in enumerate(self.hand, 1):
            print(f"{i}. {card}")
        print(f"能量：{self.energy}/{self.max_energy} | HP：{self.hp}")

# 遊戲
print("=" * 50)
print("        🃏 卡牌RPG 🃏")
print("=" * 50)

player_name = input("玩家名稱：")
player = Player(player_name)
computer = Player("電腦")

# 初始抽牌
player.draw_card(4)
computer.draw_card(4)

# 遊戲回合
round_num = 1
while player.hp > 0 and computer.hp > 0:
    print(f"\n{'='*50}")
    print(f"第 {round_num} 回合")
    print(f"{'='*50}")
    
    # 恢復能量
    player.energy = min(player.max_energy, player.energy + 1)
    computer.energy = min(computer.max_energy, computer.energy + 1)
    
    # 抽牌
    player.draw_card(1)
    computer.draw_card(1)
    
    # 玩家回合
    print(f"\n電腦：HP {computer.hp} | 能量 {computer.energy}")
    player.show_hand()
    
    if player.hand:
        try:
            choice = int(input("\n選擇卡牌 (0 跳過)："))
            if 1 <= choice <= len(player.hand):
                card = player.hand[choice - 1]
                if card.cost <= player.energy:
                    player.energy -= card.cost
                    
                    if card.card_type == "攻擊":
                        damage = card.attack + random.randint(0, 2)
                        computer.hp = max(0, computer.hp - damage)
                        print(f"\n使用 {card.name}！造成 {damage} 傷害！")
                    elif card.card_type == "防禦":
                        print(f"\n使用 {card.name}！")
                    elif card.card_type == "法術":
                        if card.attack > 0:
                            computer.hp = max(0, computer.hp - card.attack)
                            print(f"\n使用 {card.name}！造成 {card.attack} 傷害！")
                        else:
                            heal = -card.attack
                            player.hp = min(30, player.hp + heal)
                            print(f"\n使用 {card.name}！恢復 {heal} HP！")
                    
                    player.hand.remove(card)
                else:
                    print("\n能量不足！")
        except ValueError:
            print("\n跳過")

    # 電腦回合
    if computer.hand and computer.energy > 0:
        playable = [c for c in computer.hand if c.cost <= computer.energy]
        if playable:
            card = random.choice(playable)
            computer.energy -= card.cost
            
            if card.card_type == "攻擊":
                damage = card.attack + random.randint(0, 2)
                player.hp = max(0, player.hp - damage)
                print(f"\n電腦使用 {card.name}！造成 {damage} 傷害！")
            elif card.card_type == "法術" and card.attack > 0:
                player.hp = max(0, player.hp - card.attack)
                print(f"\n電腦使用 {card.name}！造成 {card.attack} 傷害！")
            else:
                print(f"\n電腦使用 {card.name}！")
    
    print(f"\n結果：玩家 HP={player.hp} | 電腦 HP={computer.hp}")
    
    if player.hp <= 0 or computer.hp <= 0:
        break
    
    round_num += 1

# 結果
print("\n" + "=" * 50)
if player.hp > 0:
    print("🎉 你獲勝了！")
else:
    print("😢 你輸了...")
print("=" * 50)
```

---

## 12.8 本章小結

| 概念 | 重點 |
|------|------|
| 類別與物件 | 類別是模板，物件是實體 |
| 封裝 | 將資料和方法包在一起 |
| 繼承 |  子類繼承父類的屬性和方法 |
| 多型 | 不同物件對相同訊息有不同回應 |
| 建構式 | `__init__` 初始化物件狀態 |
| 屬性與方法 | 描述物件的特性和行為 |

---

## 練習題

### 基礎題

1. **簡單類別**：建立一個 `Car` 類別，有品牌、顏色屬性和方法。
2. **矩陣類別**：建立 `Matrix` 類別支援矩陣加法和乘法。
3. **銀行帳戶**：建立 `Account` 類別，實作存款、提款功能。

### 進階題

1. **形狀類別**：建立 `Shape` 父類別和 `Circle`、`Rectangle` 子類別。
2. **遊戲角色**：建立角色類別系統，支援不同職業和能力。
3. **資料管理**：建立類別管理學生資料，包含新增、刪除、查詢功能。

### 挑戰題

1. **卡片遊戲**：實作完整的卡片遊戲類別系統。
2. **庫存系統**：建立商品和訂單管理的類別層次。

---

## 進一步閱讀

### 類別特殊方法

```python
class Person:
    def __init__(self, name, age):
        self.name = name
        self.age = age
    
    def __str__(self):           # str() 輸出
        return f"{self.name}, {self.age} 歲"
    
    def __repr__(self):          # 官方表示
        return f"Person('{self.name}', {self.age})"
    
    def __eq__(self, other):     # == 比較
        return self.name == other.name and self.age == other.age
    
    def __lt__(self, other):     # < 比較
        return self.age < other.age
    
    def __len__(self):           # len() 函式
        return len(self.name)
```

### 類別屬性與靜態方法

```python
class Counter:
    count = 0                    # 類別屬性（所有實例共用）
    
    def __init__(self):
        Counter.count += 1       # 每次建立實例 count +1
    
    @classmethod
    def get_count(cls):         # 類別方法
        return cls.count
    
    @staticmethod
    def is_valid(n):            # 靜態方法
        return n > 0
```

### 描述器 (Descriptor)

```python
class Positive:
    def __init__(self):
        self.values = {}
    
    def __get__(self, obj, objtype=None):
        return self.values.get(obj, 0)
    
    def __set__(self, obj, value):
        if value < 0:
            raise ValueError("必須為正數")
        self.values[obj] = value

class Number:
    x = Positive()
    y = Positive()
```

### 抽象基底類別 (ABC)

```python
from abc import ABC, abstractmethod

class Shape(ABC):
    @abstractmethod
    def area(self):
        pass
    
    @abstractmethod
    def perimeter(self):
        pass

class Circle(Shape):
    def __init__(self, radius):
        self.radius = radius
    
    def area(self):
        return 3.14 * self.radius ** 2
```

### Python 官方文件

- [類別](https://docs.python.org/3/tutorial/classes.html) - 官方類別教學
- [特殊方法名稱](https://docs.python.org/3/reference/datamodel.html#special-method-names) - 特殊方法完整列表
- [abc 模組](https://docs.python.org/3/library/abc.html) - 抽象基底類別

---

*下一章節，我們將學習第 13 章模組與套件，這是 Python 程式設計的重要概念。*