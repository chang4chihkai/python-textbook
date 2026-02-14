# 第 8 章｜字串處理

## 學習目標

- 掌握字串的基本操作
- 學會使用字串的各種方法
- 理解格式化字串的技巧
- 學習正規表達式的基本用法

---

## 8.1 字串基礎複習

> **💡 Tip（小技巧）**：在 Python 中，可以使用 f-string 來進行字串格式化，這是一種簡潔且易讀的方式。例如：`f"Hello, {name}"`

### 建立字串

```python
# 單引號、雙引號都可以
s1 = 'Hello'
s2 = "Hello"

# 三引號用于多行字串
s3 = """這是
多行
字串"""

# 轉義字元
s4 = "Hello\nWorld"  # 換行
s5 = "Hello\tWorld"  # Tab
s6 = "He said \"Hi\"" # 雙引號內嵌
```

### 字串是不可變的

```python
s = "Hello"
# s[0] = "h"  # 錯誤！字串不可修改

# 若要修改，需要建立新的字串
s = "h" + s[1:]
print(s)   # hello
```

---

## 8.2 字串切片

### 基本切片

```python
s = "Hello World"

print(s[0:5])      # Hello（索引 0 到 4）
print(s[6:])       # World（索引 6 到結束）
print(s[:5])       # Hello（開頭到索引 4）
print(s[::2])      # HloWrd（間隔 2）
print(s[::-1])     # dlroW olleH（反轉）
print(s[-5:])      # World（倒數 5 個字元）
```

---

## 8.3 字串方法

### 大小寫轉換

```python
s = "Hello World"

print(s.upper())          # HELLO WORLD（全部大寫）
print(s.lower())          # hello world（全部小寫）
print(s.capitalize())     # Hello world（首字大寫）
print(s.title())          # Hello World（每個單字首字大寫）
print(s.swapcase())       # hELLO wORLD（大小寫互換）
```

### 搜尋與取代

```python
s = "Hello World"

print(s.find("World"))      # 6（找到的位置）
print(s.find("Python"))     # -1（沒找到）
print(s.index("World"))     # 6（類似 find）
print(s.count("l"))         # 3（計算出現次數）

s2 = s.replace("World", "Python")
print(s2)                   # Hello Python（取代）
print(s.replace("l", "L")) # HeLLo WorLd（取代所有）
```

### 判斷方法

```python
s = "Hello123"

print(s.isalpha())      # False（是否全為字母）
print(s.isdigit())      # False（是否全為數字）
print(s.isalnum())      # True（是否為字母或數字）
print(s.isupper())      # False（是否全大寫）
print(s.islower())      # False（是否全小寫）
print(s.isspace())      # False（是否為空白）

s2 = "   "
print(s2.isspace())     # True
```

### 去除空白

```python
s = "   Hello World   "

print(s.strip())        # Hello World（去除兩端空白）
print(s.lstrip())       # Hello World   （去除左側空白）
print(s.rstrip())       #    Hello World（去除右側空白）

s2 = "xxxHelloxxx"
print(s2.strip("x"))   # Hello（去除指定的字元）
```

### 分割與結合

```python
s = "apple,banana,cherry"

# split - 分割成串列
print(s.split(","))    # ['apple', 'banana', 'cherry']

s2 = "Hello World"
print(s2.split())      # ['Hello', 'World']

# join - 結合成字串
words = ["apple", "banana", "cherry"]
print(",".join(words)) # apple,banana,cherry
print("-".join(words)) # apple-banana-cherry

# 實際應用：行號處理
lines = "第一行\n第二行\n第三行"
for i, line in enumerate(lines.split("\n"), 1):
    print(f"{i}: {line}")
```

---

## 8.4 字串格式化

### f-string（Python 3.6+）

```python
name = "小明"
age = 20
score = 85.5

# f-string（最推薦）
print(f"姓名：{name}，年齡：{age}")
print(f"成績：{score:.1f}")        # 85.5（格式化小數）
print(f"年齡兩年後：{age + 2}")

# 對齊
print(f"{name:>10}")    #       小明（右對齊，寬度10）
print(f"{name:<10}")    # 小明       （左對齊）
print(f"{name:^10}")    #    小明    （置中）
```

### format 方法

```python
print("姓名：{}，年齡：{}".format("小明", 20))
print("姓名：{0}，年齡：{1}".format("小明", 20))
print("姓名：{name}，年齡：{age}".format(name="小明", age=20))
print("成績：{:.2f}".format(85.567))  # 85.57
```

### 舊式格式化

```python
# % 格式化（Python 2 風格）
name = "小明"
score = 85
print("姓名：%s，成績：%d" % (name, score))
print("成績：%.1f" % score)   # 85.5
```

---

## 8.5 正規表達式入門

### 什麼是正規表達式？

**正規表達式（Regular Expression）** 是用來匹配字串樣式的強大工具。

```python
import re
```

### 基本匹配

```python
text = "我的電話是 0912-345-678，電子郵件是 test@example.com"

# 搜尋數字
numbers = re.findall(r"\d+", text)
print(numbers)  # ['0912', '345', '678']

# 搜尋特定格式
phone = re.findall(r"\d{4}-\d{3}-\d{3}", text)
print(phone)    # ['0912-345-678']

# 搜尋 Email
email = re.findall(r"\w+@\w+\.\w+", text)
print(email)    # ['test@example.com']
```

### 常用符號

| 符號 | 意義 | 範例 |
|------|------|------|
| `.` | 任意字元 | `a.c` 匹配 "abc" |
| `\d` | 數字 | `\d+` 匹配 "123" |
| `\w` | 字母數字底線 | `\w+` 匹配 "abc123" |
| `\s` | 空白 | 匹配空格、TAB |
| `*` | 0次或多次 | `ab*` 匹配 "a", "ab", "abb" |
| `+` | 1次或多次 | `ab+` 匹配 "ab", "abb" |
| `?` | 0次或1次 | `ab?` 匹配 "a", "ab" |
| `{n}` | n次 | `\d{4}` 匹配 4 位數 |
| `{n,m}` | n到m次 | `\d{3,4}` 匹配 3-4 位數 |
| `^` | 開頭 | `^Hello` |
| `$` | 結尾 | `World$` |
| `[]` | 字元集 | `[aeiou]` 母音 |
| `\|` | 或 | `cat\|dog` |

### 替換與分割

```python
text = "Hello   World!"

# 用正規表達式替換
result = re.sub(r"\s+", " ", text)  # 多個空白換成一個
print(result)   # Hello World!

# 用正規表達式分割
text = "apple,banana;cherry;orange"
result = re.split(r"[;,]", text)
print(result)   # ['apple', 'banana', 'cherry', 'orange']
```

---

## 8.6 Turtle 繪圖：用字串格式化畫圖

學會了字串，我們可以用 f-string 來動態產生圖形描述，讓畫圖更加靈活！

### 用 f-string 產生座標

```python
import turtle

# 用 f-string 產生座標描述
x, y = 50, 100

# 直接在 goto 中使用變數
turtle.goto(x, y)

# 用 f-string 產生移動指令
for i in range(4):
    turtle.forward(80)
    turtle.right(90)

turtle.done()
```

### 根據使用者名字畫圖

```python
import turtle

name = input("請輸入你的名字：")

# 用 f-string 動態設定顏色
if name:
    first_letter = name[0].upper()
    turtle.write(f"Hello, {name}!", align="center", font=("Arial", 20, "bold"))
else:
    turtle.write("Hello, World!", align="center", font=("Arial", 20, "bold"))

turtle.done()
```

### 用字串切片畫圖

```python
import turtle

# 用字串切片來控制烏龜
text = "RRLLRRLL"  # R=右轉, L=左轉
angle = 90
length = 50

for char in text:
    if char == "R":
        turtle.right(angle)
    elif char == "L":
        turtle.left(angle)
    turtle.forward(length)

turtle.done()
```

### 用 split 分割指令

```python
import turtle

# 用分號分割多個指令
commands = "forward(50);right(90);forward(50);right(90)"

# 分割並執行
for cmd in commands.split(";"):
    if "forward" in cmd:
        # 從 "forward(50)" 取出數字
        num = cmd.split("(")[1].split(")")[0]
        turtle.forward(int(num))
    elif "right" in cmd:
        num = cmd.split("(")[1].split(")")[0]
        turtle.right(int(num))

turtle.done()
```

### 練習：畫出名字的形狀

```python
import turtle

name = input("請輸入你的名字：")

# 讓烏龜寫出名字
turtle.penup()
turtle.goto(0, 50)
turtle.pendown()
turtle.write(name, align="center", font=("Arial", 30, "bold"))

# 用名字的長度來決定畫什麼
length = len(name) * 10

for i in range(4):
    turtle.forward(length)
    turtle.right(90)

turtle.done()
```

---

## 8.7 實用範例

### 範例1：密碼驗證

```python
import re

def validate_password(password):
    """驗證密碼強度"""
    errors = []
    
    if len(password) < 8:
        errors.append("密碼至少 8 個字元")
    if not re.search(r"[A-Z]", password):
        errors.append("密碼需包含大寫字母")
    if not re.search(r"[a-z]", password):
        errors.append("密碼需包含小寫字母")
    if not re.search(r"\d", password):
        errors.append("密碼需包含數字")
    
    if errors:
        return False, errors
    return True, ["密碼強度 OK"]

# 測試
pw = input("請輸入密碼：")
valid, message = validate_password(pw)
print(message)
```

### 範例2：電話號碼格式化

```python
import re

def format_phone(phone):
    """將電話號碼格式化為 0912-345-678"""
    # 移除所有非數字字元
    digits = re.sub(r"\D", "", phone)
    
    # 檢查是否為 10 位數
    if len(digits) == 10:
        return f"{digits[:4]}-{digits[4:7]}-{digits[7:]}"
    return "無效的電話號碼"

# 測試
phones = ["0912345678", "0912-345-678", "(02)1234-5678"]
for p in phones:
    print(f"{p} -> {format_phone(p)}")
```

### 範例3：文字清洗

```python
import re

def clean_text(text):
    """清洗文字：移除多餘空白、統一格式"""
    # 移除多餘空白
    text = re.sub(r"\s+", " ", text)
    # 移除首尾空白
    text = text.strip()
    # 將句點後加上空格
    text = re.sub(r"\.([A-Z])", r". \1", text)
    return text

dirty = "   Hello   World   .This   is   a   test.   "
print(clean_text(dirty))  # Hello World. This is a test.
```

---

## 本章小結

| 方法 | 說明 |
|------|------|
| `upper()`, `lower()` | 大小寫轉換 |
| `strip()` | 去除空白 |
| `split()`, `join()` | 分割與結合 |
| `find()`, `replace()` | 搜尋與取代 |
| `f"{x}"` | 格式化字串 |

| 正規表達式 | 意義 |
|------------|------|
| `\d` | 數字 |
| `\w` | 字母數字 |
| `+` | 1 次或多次 |
| `*` | 0 次或多次 |
| `[]` | 字元集 |

---

## 8.7 實用範例 - 小遊戲

### 遊戲 1：文字密碼解謎遊戲

使用正規表達式設計的密碼解謎遊戲！

```python
# 文字密碼解謎遊戲
# 學習重點：字串操作、正規表達式、字串格式化

import re

print("=" * 50)
print("        🔐 密碼解謎遊戲 🔐")
print("=" * 50)
print()
print("解開密碼線索，找出隐藏的訊息！")
print()

# 謎題資料
puzzles = [
    {
        "clue": "電話號碼",
        "text": "我的電話是 0912-345-678，歡迎打給我！",
        "pattern": r"\d{4}-\d{3}-\d{3}",
        "answer": "0912-345-678"
    },
    {
        "clue": "電子郵件",
        "text": "請寄信到 test@example.com 給我",
        "pattern": r"\w+@\w+\.\w+",
        "answer": "test@example.com"
    },
    {
        "clue": "網址",
        "text": "我的網站是 https://www.example.com/index.html",
        "pattern": r"https?://[^\s]+",
        "answer": "https://www.example.com/index.html"
    },
    {
        "clue": "IP地址",
        "text": "伺服器IP是 192.168.1.100，請連線",
        "pattern": r"\d{1,3}\.\d{1,3}\.\d{1,3}\.\d{1,3}",
        "answer": "192.168.1.100"
    },
    {
        "clue": "日期",
        "text": "活動日期是 2024/12/25，歡迎參加！",
        "pattern": r"\d{4}/\d{1,2}/\d{1,2}",
        "answer": "2024/12/25"
    }
]

# 顯示謎題
for i, puzzle in enumerate(puzzles, 1):
    print(f"謎題 {i}：尋找{puzzle['clue']}")
    print(f"原文：{puzzle['text']}")
    print()
    
    # 使用正規表達式找出答案
    matches = re.findall(puzzle["pattern"], puzzle["text"])
    
    if matches:
        print(f"找到的{puzzle['clue']}：{matches[0]}")
        
        # 玩家回答
        answer = input("這是正確答案嗎？(y/n)：")
        if answer.lower() == "y":
            print("✅ 答對了！")
        else:
            print(f"❌ 不對，正確答案是：{puzzle['answer']}")
    else:
        print("找不到答案...")
    
    print("-" * 50)
    print()

print()
print("🎉 恭喜完成所有謎題！")

# 隱藏訊息遊戲
print()
print("=" * 50)
print("        🔍  Bonus：隱藏訊息遊戲 🔍")
print("=" * 50)
print()

# 隱藏訊息
secret_message = "Python程式設計超有趣！"
coded_message = ""

# 編碼：每隔一個字取一個
for i in range(0, len(secret_message), 2):
    coded_message = coded_message + secret_message[i]

print(f"編碼後的訊息：{coded_message}")
print()
print("提示：這是每隔一個字取出的結果")
print()

# 解碼
decoded = ""
for i in range(len(coded_message)):
    decoded = decoded + coded_message[i]
    if i < len(secret_message) - 1:
        decoded = decoded + "*"

print(f"解碼嘗試：{decoded}")
```

---

### 遊戲 2：文字冒險遊戲（增強版）

使用豐富字串處理的文字冒險遊戲！

```python
# 文字冒險遊戲 - 強化版
# 學習重點：字串操作、輸入驗證、格式化輸出

import random
import time

print("=" * 60)
print("           🗡️ 文字冒險：光明與黑暗 🗡️")
print("=" * 60)
print()

# 玩家設定
player_name = input("勇者，請輸入你的名字：")
player_hp = 100
player_attack = 20
player_gold = 50
inventory = ["新手劍", "麵包"]

print()
print(f"歡迎，{player_name}！你的冒險即將開始...")
time.sleep(1)

# 怪物資料
monsters = [
    {"name": "哥布林", "hp": 30, "attack": 10, "gold": 15},
    {"name": "史萊姆", "hp": 20, "attack": 5, "gold": 10},
    {"name": "狼", "hp": 40, "attack": 15, "gold": 25},
    {"name": "半獸人", "hp": 50, "attack": 20, "gold": 30}
]

# 道具商店
shop = {
    "HP藥水": {"price": 30, "effect": "回覆 50 HP"},
    "力量戒指": {"price": 100, "effect": "攻擊力 +10"},
    "黃金劍": {"price": 200, "effect": "攻擊力 +30"},
    "聖杯": {"price": 500, "effect": "完全康復"}
}

def show_status():
    """顯示玩家狀態"""
    print()
    print("-" * 40)
    print(f"勇者：{player_name}")
    print(f"生命：{player_hp} / 100")
    print(f"攻擊：{player_attack}")
    print(f"金幣：{player_gold}")
    print(f"背包：{', '.join(inventory)}")
    print("-" * 40)

def battle():
    """戰鬥"""
    global player_hp, player_gold
    
    monster = random.choice(monsters).copy()
    monster_hp = monster["hp"]
    
    print()
    print("⚔️ 遭遇戰鬥！")
    print(f"敵人：{monster['name']} (HP: {monster_hp})")
    
    while monster_hp > 0 and player_hp > 0:
        print()
        print(f"{player_name}: {player_hp} HP | {monster['name']}: {monster_hp} HP")
        print("1. 攻擊  2. 使用道具  3. 逃跑")
        
        choice = input("選擇行動：")
        
        if choice == "1":
            # 攻擊
            damage = random.randint(player_attack - 5, player_attack + 5)
            monster_hp = monster_hp - damage
            print(f"\n你攻擊了 {monster['name']}，造成 {damage} 傷害！")
            
            if monster_hp <= 0:
                break
            
            # 怪物反擊
            enemy_damage = random.randint(monster["attack"] - 3, monster["attack"] + 3)
            player_hp = player_hp - enemy_damage
            print(f"{monster['name']} 反擊，造成 {enemy_damage} 傷害！")
            
        elif choice == "2":
            # 使用道具
            if len(inventory) == 0:
                print("\n背包是空的！")
            else:
                print(f"\n背包：{', '.join(inventory)}")
                item = input("使用哪個道具？")
                
                if item in inventory:
                    if item == "麵包":
                        player_hp = min(100, player_hp + 20)
                        inventory.remove(item)
                        print("\n你吃了麵包，恢復了 20 HP！")
                    elif item == "HP藥水":
                        player_hp = min(100, player_hp + 50)
                        inventory.remove(item)
                        print("\n你喝了 HP藥水，恢復了 50 HP！")
                    else:
                        print("\n無法使用這個道具")
                else:
                    print("\n背包中沒有這個道具")
                    
        elif choice == "3":
            # 逃跑
            if random.random() > 0.5:
                print("\n你成功逃跑了！")
                return
            else:
                print("\n逃跑失敗！")
                enemy_damage = monster["attack"]
                player_hp = player_hp - enemy_damage
                print(f"{monster['name']} 攻擊你，造成 {enemy_damage} 傷害！")
        else:
            print("\n無效的選擇！")
    
    if player_hp <= 0:
        print("\n💀 你被打敗了...")
        print("遊戲結束")
        return False
    else:
        gold_gained = monster["gold"]
        player_gold = player_gold + gold_gained
        print(f"\n🎉 你打敗了 {monster['name']}！")
        print(f"獲得 {gold_gained} 金幣！")
        return True

def visit_shop():
    """商店"""
    global player_gold, player_attack, player_hp
    
    print("\n🏪 歡迎來到商店！")
    print("-" * 40)
    
    for item, info in shop.items():
        print(f"{item}: {info['price']} 金幣 - {info['effect']}")
    
    print(f"\n你目前有 {player_gold} 金幣")
    
    item = input("\n要買什麼？(輸入名稱，直接 Enter 離開)：")
    
    if item in shop:
        price = shop[item]["price"]
        if player_gold >= price:
            player_gold = player_gold - price
            
            if item == "HP藥水":
                player_hp = 100
                print("\n聖杯發揮功效，你完全康復了！")
            elif item == "力量戒指":
                player_attack = player_attack + 10
                print("\n你戴上了力量戒指！")
            elif item == "黃金劍":
                player_attack = player_attack + 30
                print("\n你拿起了黃金劍！")
            
            inventory.append(item)
            print(f"購買成功！剩餘金幣：{player_gold}")
        else:
            print("\n金幣不足！")
    else:
        print("\n離開商店")

# 遊戲主迴圈
day = 1
while player_hp > 0:
    print()
    print("=" * 60)
    print(f"第 {day} 天")
    print("=" * 60)
    
    show_status()
    
    print("\n選項：")
    print("1. 探索森林  2. 訪問商店  3. 休息  4. 離開遊戲")
    
    choice = input("選擇行動：")
    
    if choice == "1":
        # 探索
        outcome = random.random()
        if outcome < 0.6:
            # 戰鬥
            result = battle()
            if result == False:
                break
        elif outcome < 0.8:
            # 發現寶箱
            gold_found = random.randint(10, 30)
            player_gold = player_gold + gold_found
            print(f"\n💰 你發現了寶箱，獲得 {gold_found} 金幣！")
        else:
            # 什麼都沒有
            print("\n🌲 你在森林中漫步，但什麼都沒發現...")
            
    elif choice == "2":
        visit_shop()
        
    elif choice == "3":
        # 休息
        player_hp = min(100, player_hp + 30)
        print(f"\n😴 你休息了一晚，恢復了 30 HP！")
        
    elif choice == "4":
        print("\n感謝遊玩！")
        break
    
    day = day + 1
    time.sleep(0.5)

print()
print("=" * 60)
print("        📜 遊戲結束 📜")
print("=" * 60)
print(f"你存活了 {day - 1} 天")
print(f"最終擁有 {player_gold} 金幣")
```

---

## 8.8 本章小結

### 基礎題

1. **大小寫轉換**：輸入一句話，分別輸出全大寫和全小寫。
2. **字串反轉**：反轉輸入的字串。
3. **字數統計**：統計字串中每個字元出現次數。
4. **去除空白**：使用 strip() 去除字串兩端空白。
5. **字串分割**：將「apple,banana,cherry」用逗號分割成串列。
6. **字串結合**：將串列 ["a", "b", "c"] 用 "-" 連接成字串。
7. **子字串搜尋**：判斷「hello」是否包含「ll」。
8. **字串取代**：將「I like cat」中的「cat」取代為「dog」。
9. **首字大寫**：將「hello world」轉換為「Hello World」。
10. **判斷開頭結尾**：判斷字串是否以「http」開頭或以「.com」結尾。

### 進階題

1. **密碼驗證**：參考範例 1，實作密碼驗證。
2. **Email 擷取**：從一段文字中找出所有 Email 位址。
3. **電話格式化**：參考範例 2，格式化不同格式的電話號碼。
4. **網址解析**：解析 URL 取得通訊協定、網域、路徑。
5. **簡體轉繁體**：使用字典對照表轉換簡體中文為繁體。
6. **URL 解析**：從 URL 中提取 protocol、domain、port、path。
7. **文字清洗**：移除文字中的特殊字元，只保留英數字。
8. **密碼強度檢查**：檢查密碼是否包含大寫、小寫、數字和特殊符號。

### 挑戰題

1. **CSV 解析**：解析 CSV 格式字串為二維串列。
2. **模板引擎**：實作簡單的模板替換功能。
3. **Markdown 轉 HTML**：將簡單的 Markdown 語法轉換為 HTML。

---

## 進一步閱讀

### 字串常用方法

```python
s = "Hello, Python!"

# 大小寫轉換
s.upper()           # "HELLO, PYTHON!"
s.lower()           # "hello, python!"
s.title()           # "Hello, Python!"
s.capitalize()     # "Hello, python!"
s.swapcase()       # "hELLO, pYTHON!"

# 搜尋與取代
s.find("Python")    # 找到回傳索引 → 7
s.index("Python")   # 同 find，找不到會錯誤
s.count("o")        # 計算出現次數 → 2
s.replace("Python", "World")  # "Hello, World!"

# 分割與合併
s.split(",")        # ['Hello', ' Python!']
"-".join(['a', 'b', 'c'])  # "a-b-c"

# 去除空白
s.strip()           # 去除兩端空白
s.lstrip()          # 去除左側
s.rstrip()          # 去除右側
```

### 正規表達式 (re 模組)

```python
import re

text = "我的電話是 0912-345-678，email 是 test@example.com"

# 搜尋模式
re.findall(r"\d+", text)    # ['0912', '345', '678']
re.findall(r"[\w.]+@[\w.]+", text)  # ['test@example.com']

# 取代
re.sub(r"\d{4}-\d{3}-\d{3}", "[電話號碼]", text)
# "我的電話是 [電話號碼]，email 是 test@example.com"

# 分割
re.split(r"[,\s]+", "a,b c d")  # ['a', 'b', 'c', 'd']
```

### f-string 進階用法

```python
name = "Alice"
age = 25

# 基本用法
f"{name} is {age}"           # "Alice is 25"

# 格式化
f"{age:05d}"                 # "00025" - 補零
f"{3.14159:.2f}"             # "3.14" - 浮點數格式
f"{name!r}"                  # "'Alice'" - repr 格式

# 巢狀引用
d = {"key": "value"}
f"{d['key']}"                # "value"
```

### Python 官方文件

- [字串方法](https://docs.python.org/3/library/stdtypes.html#string-methods) - 所有字串方法
- [re 模組](https://docs.python.org/3/library/re.html) - 正規表達式
- [格式化字串](https://docs.python.org/3/library/string.html#formatstrings) - 格式化規格

---

*下一章節，我們將學習檔案操作，讓程式能夠讀寫檔案。*
