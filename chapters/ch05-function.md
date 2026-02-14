# 第 5 章｜函式

## 學習目標

- 理解函式的概念與優點
- 掌握定義和呼叫函式的方法
- 學會使用參數和回傳值
- 理解變數作用域的概念
- 能夠設計自己的函式

---

## 5.1 為什麼需要函式？

> **📝 Note（說明）**：在 Python 中，所有資料（包括數字和字串）實際上都是物件（Object）。變數本質上是引用（reference）物件的指標。

假設你需要計算多個圓的面積：

```
# 沒有使用函式
r1 = 5
area1 = 3.14 * r1 * r1
print("面積1：", area1)

r2 = 10
area2 = 3.14 * r2 * r2
print("面積2：", area2)

r3 = 3
area3 = 3.14 * r3 * r3
print("面積3：", area3)
```

重複寫了相同的公式好幾次！如果用**函式（Function）**，可以將公式包裝起來，重複使用：

```python
# 使用函式
def circle_area(r):
    return 3.14 * r * r

print("面積1：", circle_area(5))
print("面積2：", circle_area(10))
print("面積3：", circle_area(3))
```

---

## 5.2 定義函式

### 基本語法

```python
def 函式名稱(參數):
    """文件字串（可選）"""
    # 函式內容
    return 回傳值    # （可選）
```

### 範例：打招呼函式

```python
def say_hello():
    print("你好！")

# 呼叫函式
say_hello()
say_hello()
say_hello()
```

執行結果：
```
你好！
你好！
你好！
```

---

## 5.3 參數

### 有參數的函式

```python
def greet(name):
    print("你好，" + name + "！")

greet("小明")
greet("小華")
```

執行結果：
```
你好，小明！
你好，小小華！
```

### 預設參數

可以設定參數的預設值：

```python
def greet(name, greeting="你好"):
    print(greeting + "，" + name + "！")

greet("小明")           # 使用預設值
greet("小華", "早安")   # 指定 greeting
```

執行結果：
```
你好，小明！
早安，小華！
```

### 多個參數

```python
def add(a, b):
    result = a + b
    print(a, "+", b, "=", result)

add(3, 5)
add(10, 20)
```

---

## 5.4 回傳值

使用 `return` 將計算結果傳回：

```python
def circle_area(r):
    return 3.14 * r * r

# 將回傳值存入變數
area1 = circle_area(5)
area2 = circle_area(10)

print("總面積：", area1 + area2)
```

執行結果：
```
總面積： 392.5
```

### 沒有 return 的函式

沒有 `return` 的函式會回傳 `None`：

```python
def print_hello():
    print("Hello")

result = print_hello()
print("回傳值是：", result)
```

執行結果：
```
Hello
回傳值是： None
```

### 提前結束函式

可以使用 `return` 提前結束函式：

```python
def find_even(numbers):
    for n in numbers:
        if n % 2 == 0:
            return n    # 找到第一個偶數就回傳
    return None         # 沒找到

print(find_even([1, 3, 5, 6, 7]))   # 6
print(find_even([1, 3, 5, 7]))      # None
```

---

## 5.5 變數作用域

### 區域變數 vs 全域變數

```python
x = 10    # 全域變數

def test():
    x = 5     # 區域變數（在函式內）
    print("函式內：", x)

test()
print("函式外：", x)
```

執行結果：
```
函式內： 5
函式外： 10
```

### 使用 global 存取全域變數

```python
x = 10

def test():
    global x    # 宣告要使用全域變數
    x = 5
    print("修改後：", x)

test()
print("函式外：", x)
```

執行結果：
```
修改後： 5
函式外： 5
```

**建議**：盡量避免使用 `global`，以免造成程式碼難以理解和維護。

---

## 5.6 Turtle 繪圖：用函式畫圖

學會了函式，我們就可以把畫圖的動作包裝成一個個函数，這樣可以重複使用畫出各種圖案！

### 畫正方形的函式

```python
import turtle

def draw_square(length):
    """畫出一個正方形"""
    for i in range(4):
        turtle.forward(length)
        turtle.right(90)

# 畫三個不同大小的正方形
draw_square(50)
turtle.penup()
turtle.goto(100, 0)
turtle.pendown()
draw_square(100)
turtle.penup()
turtle.goto(250, 0)
turtle.pendown()
draw_square(150)

turtle.done()
```

### 畫多邊形的函式

```python
import turtle

def draw_polygon(sides, length):
    """畫出多邊形"""
    angle = 360 / sides
    for i in range(sides):
        turtle.forward(length)
        turtle.right(angle)

# 畫出各種多邊形
draw_polygon(3, 100)   # 三角形
turtle.penup()
turtle.goto(150, 0)
turtle.pendown()
draw_polygon(4, 80)    # 正方形
turtle.penup()
turtle.goto(280, 0)
turtle.pendown()
draw_polygon(5, 70)    # 五邊形
turtle.penup()
turtle.goto(400, 0)
turtle.pendown()
draw_polygon(6, 60)    # 六邊形

turtle.done()
```

### 畫星星的函式

```python
import turtle

def draw_star(size):
    """畫出一顆星星"""
    for i in range(5):
        turtle.forward(size)
        turtle.right(144)  # 星星的角度

# 畫出三顆不同大小的星星
draw_star(50)
turtle.penup()
turtle.goto(100, 50)
turtle.pendown()
draw_star(80)
turtle.penup()
turtle.goto(220, 80)
turtle.pendown()
draw_star(100)

turtle.done()
```

### 練習：建立自己的繪圖函式庫

```python
import turtle

def draw_square(length):
    """畫正方形"""
    for i in range(4):
        turtle.forward(length)
        turtle.right(90)

def draw_triangle(length):
    """畫三角形"""
    for i in range(3):
        turtle.forward(length)
        turtle.right(120)

def draw_circle(radius):
    """畫圓"""
    turtle.circle(radius)

def draw_flower():
    """畫一朵花"""
    for i in range(6):
        turtle.circle(30)
        turtle.right(60)

# 使用自己設計的函式來畫圖
draw_square(80)
turtle.penup()
turtle.goto(150, 0)
turtle.pendown()
draw_triangle(100)
turtle.penup()
turtle.goto(300, 0)
turtle.pendown()
draw_circle(50)

turtle.done()
```

---

## 5.7 實用範例

### 範例1：計算BMI

```python
def calculate_bmi(height, weight):
    """計算 BMI"""
    bmi = weight / (height ** 2)
    return bmi

def get_bmi_status(bmi):
    """根據 BMI 回傳體位"""
    if bmi < 18.5:
        return "過輕"
    elif bmi < 24:
        return "正常"
    elif bmi < 27:
        return "過重"
    else:
        return "肥胖"

# 測試
h = 1.7
w = 65
bmi = calculate_bmi(h, w)
status = get_bmi_status(bmi)

print(f"身高 {h}m，體重 {w}kg")
print(f"BMI：{bmi:.1f}")
print(f"體位：{status}")
```

### 範例2：驗證輸入

```python
def get_positive_number(prompt):
    """取得正數，若輸入無效則持續要求輸入"""
    while True:
        try:
            num = float(input(prompt))
            if num > 0:
                return num
            else:
                print("請輸入正數！")
        except ValueError:
            print("輸入無效，請重新輸入")

# 使用
price = get_positive_number("請輸入價格：")
quantity = get_positive_number("請輸入數量：")
print("總金額：", price * quantity)
```

---

## 5.7 實用範例 - 小遊戲

### 遊戲 1：骰子RPG遊戲

一個使用函式設計的回合制 RPG 遊戲！

```python
# 骰子RPG遊戲
# 學習重點：函式設計、參數、回傳值、模組化設計

import random
import time

# ============ 遊戲函式 ============

def roll_dice(sides=6):
    """擲骰子"""
    return random.randint(1, sides)

def create_character():
    """建立角色"""
    print()
    print("=" * 50)
    print("        🧙 建立你的角色 🧙")
    print("=" * 50)
    
    name = input("請輸入角色名稱：")
    
    print()
    print("選擇職業：")
    print("  1. 戰士 (高血量、高攻擊)")
    print("  2. 魔法師 (中等血量、高魔法)")
    print("  3. 盜賊 (高敏捷、高暴擊)")
    
    while True:
        job_choice = input("請選擇 (1/2/3)：")
        
        if job_choice == "1":
            job = "戰士"
            hp = 150
            attack = 25
            defense = 15
            magic = 5
            break
        elif job_choice == "2":
            job = "魔法師"
            hp = 100
            attack = 15
            defense = 8
            magic = 30
            break
        elif job_choice == "3":
            job = "盜賊"
            hp = 110
            attack = 20
            defense = 10
            magic = 10
            break
        else:
            print("無效的選擇！")
    
    character = {
        "name": name,
        "job": job,
        "hp": hp,
        "max_hp": hp,
        "attack": attack,
        "defense": defense,
        "magic": magic,
        "gold": 0,
        "exp": 0,
        "level": 1
    }
    
    return character

def show_status(character):
    """顯示角色狀態"""
    print()
    print("-" * 40)
    print(f"角色：{character['name']} (Lv.{character['level']})")
    print(f"職業：{character['job']}")
    print(f"生命：{character['hp']} / {character['max_hp']}")
    print(f"攻擊：{character['attack']} | 防禦：{character['defense']}")
    print(f"魔法：{character['magic']} | 金幣：{character['gold']}")
    print(f"經驗：{character['exp']}")
    print("-" * 40)

def create_monster(level):
    """建立怪物"""
    monsters = [
        {"name": "哥布林", "hp": 30, "attack": 8, "defense": 3, "exp": 20, "gold": 15},
        {"name": "狼", "hp": 40, "attack": 12, "defense": 5, "exp": 30, "gold": 20},
        {"name": "哥布林戰士", "hp": 60, "attack": 15, "defense": 8, "exp": 50, "gold": 35},
        {"name": "史萊姆", "hp": 25, "attack": 6, "defense": 2, "exp": 15, "gold": 10},
        {"name": "獸人", "hp": 80, "attack": 20, "defense": 12, "exp": 70, "gold": 50}
    ]
    
    monster = random.choice(monsters).copy()
    # 根據等級調整怪物能力
    multiplier = 1 + (level - 1) * 0.2
    monster["hp"] = int(monster["hp"] * multiplier)
    monster["max_hp"] = monster["hp"]
    monster["attack"] = int(monster["attack"] * multiplier)
    monster["defense"] = int(monster["defense"] * multiplier)
    
    return monster

def battle(character, monster):
    """戰鬥函式"""
    print()
    print("=" * 50)
    print(f"⚔️ 遭遇 {monster['name']}！")
    print("=" * 50)
    
    while character["hp"] > 0 and monster["hp"] > 0:
        # 玩家攻擊
        player_damage = max(1, character["attack"] + roll_dice(10) - monster["defense"])
        monster["hp"] = monster["hp"] - player_damage
        
        print(f"\n{character['name']} 攻擊！")
        print(f"造成 {player_damage} 傷害！")
        
        if monster["hp"] <= 0:
            print(f"\n🎉 你打敗了 {monster['name']}！")
            exp_gained = monster["exp"]
            gold_gained = monster["gold"]
            character["exp"] = character["exp"] + exp_gained
            character["gold"] = character["gold"] + gold_gained
            print(f"獲得 {exp_gained} 經驗值和 {gold_gained} 金幣！")
            break
        
        # 怪物攻擊
        enemy_damage = max(1, monster["attack"] + roll_dice(6) - character["defense"])
        character["hp"] = character["hp"] - enemy_damage
        
        print(f"\n{monster['name']} 反擊！")
        print(f"受到 {enemy_damage} 傷害！")
        
        if character["hp"] <= 0:
            print(f"\n😵 你被 {monster['name']} 打敗了...")
            return False
        
        # 顯示雙方狀態
        print(f"\n{character['name']}: {character['hp']} HP | {monster['name']}: {monster['hp']} HP")
        time.sleep(1)
    
    # 檢查升級
    exp_needed = character["level"] * 100
    if character["exp"] >= exp_needed:
        character["level"] = character["level"] + 1
        character["exp"] = character["exp"] - exp_needed
        character["max_hp"] = character["max_hp"] + 20
        character["hp"] = character["max_hp"]
        character["attack"] = character["attack"] + 5
        character["defense"] = character["defense"] + 3
        character["magic"] = character["magic"] + 3
        
        print()
        print("=" * 50)
        print(f"🎊 升級了！現在是 Lv.{character['level']}！")
        print("=" * 50)
    
    return True

def explore(character):
    """探索函式"""
    # 決定發生什麼事
    outcome = random.randint(1, 10)
    
    if outcome <= 3:
        # 遇到怪物
        monster = create_monster(character["level"])
        return battle(character, monster)
    elif outcome <= 5:
        # 找到寶箱
        gold_found = roll_dice(20) * character["level"]
        character["gold"] = character["gold"] + gold_found
        print(f"\n💰 你發現了寶箱！獲得 {gold_found} 金幣！")
        return True
    elif outcome <= 7:
        # 發現商店
        print("\n🏪 你發現了一家商店！但商店還沒開門...")
        return True
    else:
        # 什麼都沒發生
        print("\n🌲 你在森林中漫步，但什麼都沒遇到...")
        return True

# ============ 主程式 ============

print("=" * 50)
print("      🎮 骰子RPG：勇者之旅 🎮")
print("=" * 50)

# 建立角色
character = create_character()

# 顯示角色資訊
show_status(character)

# 遊戲主迴圈
round_num = 1
while character["hp"] > 0:
    print()
    action = input("按 Enter 繼續探索 (輸入 q 離開)...")
    
    if action.lower() == "q":
        break
    
    print(f"\n=== 第 {round_num} 天探索 ===")
    round_num = round_num + 1
    
    # 恢復少量生命
    if character["hp"] < character["max_hp"]:
        heal = character["level"] * 5
        character["hp"] = min(character["max_hp"], character["hp"] + heal)
        print(f"💚 休息了一下，恢復了 {heal} 點生命！")
    
    # 探索
    success = explore(character)
    
    if not success:
        break
    
    # 顯示狀態
    show_status(character)

# 遊戲結束
print()
print("=" * 50)
print("        📜 遊戲結束 📜")
print("=" * 50)
print(f"你探索了 {round_num - 1} 天")
print(f"最終等級：{character['level']}")
print(f"總金幣：{character['gold']}")
print("感謝遊玩！")
```

---

### 遊戲 2： Blackjack 二十一點（使用函式版）

使用函式模組化設計的二十一點遊戲！

```python
# 二十一點遊戲（函式版）
# 學習重點：函式設計、回傳值、參數設計

import random
import time

# ============ 輔助函式 ============

def create_deck():
    """建立一副牌"""
    suits = ["♠", "♥", "♦", "♣"]
    ranks = ["A", "2", "3", "4", "5", "6", "7", "8", "9", "10", "J", "Q", "K"]
    deck = []
    for suit in suits:
        for rank in ranks:
            deck.append({"suit": suit, "rank": rank})
    random.shuffle(deck)
    return deck

def get_card_value(card):
    """取得單張牌的點數"""
    rank = card["rank"]
    if rank in ["J", "Q", "K"]:
        return 10
    elif rank == "A":
        return 11
    else:
        return int(rank)

def calculate_score(cards):
    """計算手牌點數"""
    score = 0
    aces = 0
    
    for card in cards:
        score = score + get_card_value(card)
        if card["rank"] == "A":
            aces = aces + 1
    
    # 處理 A 的點數
    while score > 21 and aces > 0:
        score = score - 10
        aces = aces - 1
    
    return score

def print_hand(player_name, cards, hide_first=False):
    """顯示玩家的牌"""
    print(f"\n{player_name} 的牌：")
    for i, card in enumerate(cards):
        if i == 0 and hide_first:
            print("  [背面]")
        else:
            print(f"  {card['suit']}{card['rank']}")

def print_score(cards):
    """顯示點數"""
    score = calculate_score(cards)
    if score > 21:
        print(f"  → 爆牌！({score})")
    elif score == 21:
        print(f"  → 21 點！")
    else:
        print(f"  → {score} 點")

def hit(deck, hand):
    """要一張牌"""
    card = deck.pop()
    hand.append(card)
    return card

def player_turn(deck, player_hand, dealer_hand):
    """玩家的回合"""
    while True:
        print_hand("你", player_hand)
        print_score(player_hand)
        
        if calculate_score(player_hand) >= 21:
            break
        
        print("\n選項：")
        print("  1. 要牌 (Hit)")
        print("  2. 停牌 (Stand)")
        
        choice = input("請選擇：")
        
        if choice == "1":
            card = hit(deck, player_hand)
            print(f"\n你抽到了：{card['suit']}{card['rank']}")
            time.sleep(0.5)
        elif choice == "2":
            print("\n你選擇停牌！")
            break
        else:
            print("無效的選擇！")
        
        time.sleep(0.5)

def dealer_turn(deck, dealer_hand):
    """莊家的回合"""
    print("\n莊家的回合...")
    time.sleep(1)
    
    while calculate_score(dealer_hand) < 17:
        card = hit(deck, dealer_hand)
        print(f"莊家抽到了：{card['suit']}{card['rank']}")
        time.sleep(1)
    
    print_hand("莊家", dealer_hand)
    print_score(dealer_hand)

def determine_winner(player_hand, dealer_hand):
    """判定輸贏"""
    player_score = calculate_score(player_hand)
    dealer_score = calculate_score(dealer_hand)
    
    print("\n" + "=" * 40)
    print("        結果揭曉！")
    print("=" * 40)
    
    print(f"\n你的點數：{player_score}")
    print(f"莊家點數：{dealer_score}")
    
    if player_score > 21:
        print("\n💥 你爆牌了！莊家獲勝！")
        return "lose"
    elif dealer_score > 21:
        print("\n🎉 莊家爆牌了！你獲勝！")
        return "win"
    elif player_score > dealer_score:
        print("\n🎉 你獲勝！")
        return "win"
    elif player_score < dealer_score:
        print("\n😢 莊家獲勝！")
        return "lose"
    else:
        print("\n⚖️ 平手！")
        return "push"

# ============ 主程式 ============

print("=" * 50)
print("      🃏 二十一點遊戲 🃏")
print("=" * 50)
print("目標：讓點數接近 21 點，但不能超過！")

# 遊戲主迴圈
while True:
    # 建立牌組和初始牌
    deck = create_deck()
    player_hand = []
    dealer_hand = []
    
    # 發牌
    hit(deck, player_hand)
    hit(deck, player_hand)
    hit(deck, dealer_hand)
    hit(deck, dealer_hand)
    
    # 顯示初始牌面
    print("\n" + "-" * 40)
    print("新的一局開始！")
    print("-" * 40)
    
    # 顯示莊家的牌（隱藏第一張）
    print_hand("莊家", dealer_hand, hide_first=True)
    print(f"  還有一張牌...")
    
    # 玩家的回合
    player_turn(deck, player_hand, dealer_hand)
    
    # 檢查玩家是否爆牌
    if calculate_score(player_hand) <= 21:
        # 莊家的回合
        dealer_turn(deck, dealer_hand)
    
    # 判定輸贏
    result = determine_winner(player_hand, dealer_hand)
    
    # 詢問是否繼續
    print("\n" + "-")
    play_again = input("要再玩一局嗎？(y/n)：")
    if play_again.lower() != "y":
        print("\n感謝遊玩！")
        break
    
    print()

print()
print("=" * 50)
print("        遊戲結束！")
print("=" * 50)
```

---

## 5.8 本章小結

| 概念 | 說明 |
|------|------|
| `def 函式名稱():` | 定義函式 |
| 參數 | 傳入函式的資料 |
| `return` | 將結果傳回呼叫處 |
| 預設參數 | 參數的預設值 |
| 區域變數 | 只在函式內有效 |
| 全域變數 | 整個程式都能存取 |

---

## 練習題

### 基礎題

1. **你好函式**：撰寫一個函式，輸入名字後輸出「你好，XXX」。
2. **最大值**：撰寫函式，傳入三個數，回傳最大的那個。
3. **次方計算**：撰寫函式，計算 a 的 b 次方（不使用 **）。
4. **絕對值**：撰寫函式，計算數字的絕對值（不使用 abs()）。
5. **判斷偶數**：撰寫函式，傳入數字，若為偶數回傳 True，否則回傳 False。
6. **計算圓面積**：撰寫函式，傳入半徑，回傳圓面積。
7. **字串反轉**：撰寫函式，傳入字串，回傳反轉後的字串。
8. **兩個數相加**：撰寫函式，傳入兩個數，回傳它們的和。
9. **判斷正負數**：撰寫函式，傳入數字，回傳「正數」、「負數」或「零」。
10. **找較小值**：撰寫函式，傳入兩個數，回傳較小的值。

### 進階題

1. **質數判斷**：撰寫函式，判斷輸入的數是否為質數。
2. **費波那契**：撰寫函式，回傳第 n 個費波那契數列。
3. **階乘**：撰寫函式，計算 n 的階乘。
4. **最大公因數**：撰寫函式，計算兩個數的最大公因數。
5. **最小公倍數**：撰寫函式，計算兩個數的最小公倍數。
6. **迴文判斷**：撰寫函式，判斷字串是否為迴文（如「ababa」）。
7. **計算 BMI**：撰寫函式，傳入身高和體重，回傳 BMI 值。
8. **篩選質數**：撰寫函式，傳入一個數字列表，回傳其中的質數。

### 挑戰題

1. **萬年曆**：撰寫函式，輸入年月，輸出該月的日曆。
2. **計算機**：撰寫可進行 +、-、*、/ 的計算機函式，並處理除以零的錯誤。
3. **通用排序**：撰寫一個排序函式，可選擇由小到大或由大到小排序。

---

## 進一步閱讀

### 更多參數類型

```python
# 預設參數
def greet(name, greeting="Hello"):
    return f"{greeting}, {name}!"

# 關鍵字參數
def person(name, age, city="Taipei"):
    return f"{name}, {age} 歲，住 {city}"

person(age=25, name="Alice")  # 可用關鍵字指定順序

# *args 和 **kwargs
def sum_all(*args):           # 可變位置參數
    return sum(args)

def print_info(**kwargs):     # 可變關鍵字參數
    for key, value in kwargs.items():
        print(f"{key}: {value}")

sum_all(1, 2, 3, 4, 5)  # → 15
print_info(name="Bob", age=30)  # name: Bob, age: 30
```

### 匿名函式 (Lambda)

```python
# 基本語法
square = lambda x: x ** 2
square(5)  # → 25

# 搭配內建函式
numbers = [1, 2, 3, 4, 5]
sorted(numbers, key=lambda x: -x)  # [5, 4, 3, 2, 1]

# 常見用法
filter(lambda x: x > 0, [-1, 2, -3, 4])  # [2, 4]
map(lambda x: x * 2, [1, 2, 3])  # [2, 4, 6]
```

### 內建高階函式

```python
# filter - 過濾
numbers = [1, 2, 3, 4, 5, 6]
list(filter(lambda x: x % 2 == 0, numbers))  # [2, 4, 6]

# map - 轉換
list(map(lambda x: x ** 2, numbers))  # [1, 4, 9, 16, 25, 36]

# reduce - 累積
from functools import reduce
reduce(lambda x, y: x + y, numbers)  # 21
```

### 變數作用域

```python
x = "global"

def test():
    x = "local"           # 區域變數
    print(x)              # → local
    
def test2():
    global x              # 宣告為全域變數
    x = "modified"
    print(x)              # → modified
```

### Python 官方文件

- [函式定義](https://docs.python.org/3/reference/compound_stmts.html#function) - 函式詳細說明
- [lambda 表達式](https://docs.python.org/3/tutorial/controlflow.html#lambda-expressions) - lambda 教學
- [functools 模組](https://docs.python.org/3/library/functools.html) - 更多函式工具

---

*下一章節，我們將學習串列與元組，這是 Python 中最重要的資料結構之一。*
